# Data Pipeline — Step by Step

## Overview

```
Google Maps API → Raw CSV → Claude Code Cleaning → Enrichment → Supabase
   (50K-100K)              (20K-40K clean)        (5K enriched)
```

## Step 1: Google Maps Data Collection

### Option A: Outscraper (Recommended — Fastest)
- Website: outscraper.com
- Cost: ~$50-100 for 50K-100K results
- Process:
  1. Create account at outscraper.com
  2. Use "Google Maps Scraper" feature
  3. Run one search per category per city batch

**Search queries to run:**
```
dog groomer, United States
pet sitter, United States
dog walker, United States
veterinary clinic, United States
pet shop, United States
dog trainer, United States
pet boarding, United States
emergency vet, United States
```

Each returns: name, address, city, state, zip, phone, website, rating, review_count, hours, latitude, longitude, place_id, photos

### Option B: Google Places API (Cheaper but slower)
- Cost: $0.032 per place detail request
- Need to search city-by-city
- Rate limited, slower to collect

### Option C: SerpAPI Google Maps (Middle ground)
- Cost: $50/mo for 5,000 searches
- Structured JSON output
- Good for targeted city searches

## Step 2: Data Cleaning with Claude Code

### Input
Raw CSV files from Outscraper (~50K-100K rows total)

### Cleaning Prompt for Claude Code
```
I have a CSV of pet service businesses scraped from Google Maps.
Clean this data following these rules:

REMOVE rows where:
- name is empty or "N/A"
- address is empty
- city is empty or state is empty
- business is permanently closed
- business is a big box retailer: Walmart, Target, Costco, PetSmart, Petco
  (keep only independent/small businesses)
- name contains "Closed", "Coming Soon", "CLOSED"
- rating is 0 or null AND review_count is 0 (likely fake/empty listing)

DEDUPLICATE:
- Same phone number → keep highest rated
- Same exact address → keep highest rated
- Very similar names in same city (fuzzy match) → keep highest rated

NORMALIZE:
- State abbreviations → full names (CA → California)
- Phone numbers → (XXX) XXX-XXXX format
- Remove leading/trailing whitespace from all fields
- Generate URL slug from name + city: "Happy Paws Austin" → "happy-paws-austin"

ADD COLUMNS:
- state_slug: california, texas, new-york, etc.
- city_slug: austin, chicago, miami, etc.
- category_slug: map from original search to our categories

OUTPUT: Clean CSV with columns:
name, slug, category_slug, address, city, city_slug, state, state_slug, zip, lat, lng, phone, website, rating, review_count, hours_json, source_id
```

### Expected Results
- Input: 50K-100K rows
- After cleaning: 20K-40K rows
- Removal rate: ~50-60% (normal for Google Maps data)

## Step 3: Data Enrichment

### 3a. Website Crawling (Top 5K listings)
Use Crawl for AI (crawlforai.com) or Firecrawl:

```
For each provider URL, extract:
- List of services offered
- Pricing information (if visible)
- Specialties or certifications
- "About us" description
- Whether they accept specific pet types
- Whether they offer mobile/at-home services
- Social media links
```

### 3b. Claude Vision Photo Scoring
For providers with Google Maps photos:
```
Score this pet service business photo 1-5:
- Is the storefront clean and inviting?
- Can you see the business name?
- Does it look like a professional pet service?
- Return: score (1-5), description (one line)
```

### 3c. Enrichment Fields to Add
| Field | Source | Type |
|-------|--------|------|
| services | website crawl | JSONB array |
| specialties | website crawl | JSONB array |
| price_range | website crawl | "$" / "$$" / "$$$" |
| accepts_large_dogs | website crawl | boolean |
| cat_specialist | website crawl | boolean |
| emergency_24h | website crawl | boolean |
| organic_products | website crawl | boolean |
| mobile_service | website crawl | boolean |
| photo_score | Claude Vision | integer 1-5 |
| description | website crawl | text |

## Step 4: Import to Supabase

### Create tables
Run the SQL from DATABASE.md in Supabase SQL editor.

### Seed categories
```sql
INSERT INTO categories (name, slug, search_terms) VALUES
('Dog Groomers', 'dog-groomers', '["dog groomer","pet grooming","dog grooming salon"]'),
('Pet Sitters', 'pet-sitters', '["pet sitter","dog sitter","cat sitter"]'),
('Dog Walkers', 'dog-walkers', '["dog walker","dog walking service"]'),
('Veterinary Clinics', 'veterinary-clinics', '["veterinary clinic","vet","animal hospital"]'),
('Pet Shops', 'pet-shops', '["pet shop","pet store","pet supply"]'),
('Dog Trainers', 'dog-trainers', '["dog trainer","dog training","puppy training"]'),
('Pet Boarding', 'pet-boarding', '["pet boarding","dog boarding","kennel"]'),
('Emergency Vet', 'emergency-vet', '["emergency vet","24 hour vet","animal emergency"]');
```

### Seed cities (top 100 US cities)
Generate from Census data or use a public dataset of US cities with population > 100K.

### Import providers
```bash
# Convert cleaned CSV to Supabase-compatible format
node scripts/import-providers.js data/providers-clean.csv

# Or use Supabase CSV import in dashboard
```

## Step 5: Ongoing Data Freshness

### Monthly (automated cron job)
- Re-scrape Google Maps for changes (closed businesses, new businesses)
- Run cleaning pipeline on delta
- Update Supabase with changes

### Quarterly (manual 1-2h)
- Spot-check 50 random listings for accuracy
- Remove any reported incorrect listings
- Add new cities if traffic data suggests demand

### On-demand
- When a business claims their listing, they update their own data
- This is the best data source — it's free and always accurate
