# Pet Services Online Directory — Master Plan

## Vision

A niche directory of pet services (groomers, walkers, sitters, vets, pet shops) that ranks organically for "near me" searches, monetizes via ads + featured listings + affiliate, and runs passively after the initial build phase.

**Target:** $500+/mo in 6 months, zero maintenance after month 4.

**Inspiration:** Greg Isenberg & Frey Chu's method — Claude Code built a $273/day luxury restroom trailer directory in 4 days. We apply the same playbook to the pet services niche.

---

## Why Pet Services?

| Factor | Value |
|--------|-------|
| "dog groomer near me" monthly searches | 200K+ |
| "pet sitter near me" monthly searches | 90K+ |
| "vet near me" monthly searches | 300K+ |
| Keyword difficulty | Low (<20) |
| Existing dominant directory | None (Yelp is generic, Rover is marketplace-only) |
| Emotional buyer intent | Very high — pet owners search extensively |
| Pet industry size | $150B+ growing 6% yearly |
| AdSense RPM for pet niche | $8-12 (high-value) |
| Affiliate programs | Pet insurance, pet food, pet products |

---

## The Greg Isenberg / Frey Chu Playbook (Applied to Pets)

### Step 1: Keyword Research & Validation
- Use Ahrefs/Ubersuggest for "near me" keywords with 30-100K monthly searches
- Target keyword difficulty < 20
- Look for fragmented intent (no single dominant player)
- Validate: Google the keywords — if results are outdated/basic directories, there's opportunity

### Step 2: Data Collection (Google Maps Scraping)
- Scrape Google Maps using exact categories: "dog groomer", "pet sitter", "veterinary clinic", "pet shop", "dog walker"
- Cover top 50-100 US cities (or top 20 Brazilian cities for PT-BR version)
- Raw export: expect 50K-100K rows across all categories

### Step 3: Data Cleaning (Claude Code)
- Feed CSVs to Claude Code with cleaning prompts
- Remove: no name/address, permanently closed, off-niche (big box retailers, generic stores)
- Deduplicate by phone number and address
- Expected: 50K-100K → 20K-40K clean listings

### Step 4: Data Enrichment (Crawl for AI + Claude Vision)
- Crawl provider websites for: services offered, pricing indicators, specialties, certifications
- Use Claude Vision to verify/score top photos (storefront quality, clean facilities)
- Add enrichment fields: "accepts large dogs", "cat specialist", "organic products", "emergency 24h"
- This depth is what beats Yelp/Google — specialized filters that generic platforms don't have

### Step 5: Build the Directory Site
- Programmatic SEO: generate city + service pages automatically
- Example pages: "Best Dog Groomers in Austin TX", "Pet Sitters Near Me in Chicago"
- Each listing page: name, address, phone, hours, rating, reviews, photos, services, booking link
- "Claim Your Listing" CTA on every free listing

### Step 6: SEO & Launch
- Target high-volume local keywords with city/state pages
- Each state page can rank for 1,000+ keyword variations
- Internal linking structure: State → City → Service → Individual listing
- Schema.org markup for local business rich results
- Sitemap with all programmatic pages

### Step 7: Monetize
- **Phase 1 (Month 3):** AdSense on high-traffic pages
- **Phase 2 (Month 4):** Featured listings — providers pay $99-199/yr for top placement + verified badge
- **Phase 3 (Month 5):** Affiliate links — pet insurance (Lemonade, Trupanion), pet food (Chewy), pet products
- **Phase 4 (Month 6+):** Lead gen fees — $5-10 per booked appointment via directory
- **Future:** Build SaaS layer on top of directory traffic (booking system, CRM for pet businesses)

---

## Revenue Math (Month 6)

| Source | Calculation | Monthly |
|--------|------------|---------|
| AdSense | 10K visits/mo × $10 RPM | $100 |
| Featured Listings | 30 providers × $149/yr avg | $372 |
| Affiliate | Pet insurance + food referrals | $200 |
| **Total Month 6** | | **~$672/mo** |
| **Total Month 12** (SEO compounding) | 30K+ visits | **$1,200-2,500/mo** |

---

## Tech Stack

| Layer | Tool | Why |
|-------|------|-----|
| Framework | Next.js 14 (App Router) | SSG for SEO, fast, free on Vercel |
| Database | Supabase (PostgreSQL) | Free tier, great for listings |
| Hosting | Vercel | Free, auto-deploys, edge CDN |
| Data Scraping | Google Maps API + Outscraper | Bulk location data |
| Data Cleaning | Claude Code | AI-powered CSV cleaning |
| Data Enrichment | Crawl for AI + Claude Vision | Website scanning + image quality |
| SEO | Programmatic pages + Schema.org | Automated city/service pages |
| Ads | Google AdSense → Mediavine (at 50K sessions) | Revenue scales with traffic |
| Payments | Stripe | Featured listing payments |
| Email | Resend | Claim listing notifications |
| Analytics | Google Analytics 4 + Search Console | Track rankings + traffic |

---

## Implementation Phases

### Phase 1: Foundation (Week 1-2) — 20-25h
- [ ] Set up Next.js project with Supabase
- [ ] Design database schema (providers, categories, cities, reviews)
- [ ] Build seed script for Google Maps data
- [ ] Create base UI components (listing card, filter sidebar, search)
- [ ] Set up Vercel deployment

### Phase 2: Data Pipeline (Week 3) — 10-15h
- [ ] Run Google Maps scraper for 5 service categories × 50 cities
- [ ] Clean data with Claude Code (remove junk, deduplicate)
- [ ] Enrich top listings with website crawl data
- [ ] Import clean data into Supabase
- [ ] Verify data quality on 100 random listings

### Phase 3: Programmatic SEO Pages (Week 4-5) — 15-20h
- [ ] Generate state landing pages (50 states)
- [ ] Generate city + service pages (e.g., "dog-groomers-austin-tx")
- [ ] Generate individual listing pages with full details
- [ ] Add Schema.org LocalBusiness markup
- [ ] Create XML sitemap with all pages
- [ ] Submit to Google Search Console

### Phase 4: Core Features (Week 6) — 10-15h
- [ ] Search with autocomplete (city + service)
- [ ] Filter sidebar (service type, rating, distance, open now)
- [ ] "Claim Your Listing" flow (email verification)
- [ ] Contact form / click-to-call tracking
- [ ] Mobile-responsive design

### Phase 5: Monetization (Week 7-8) — 8-10h
- [ ] Integrate Google AdSense
- [ ] Build featured listing upgrade flow (Stripe checkout)
- [ ] Add affiliate links (pet insurance, Chewy, Petco)
- [ ] "Get a Quote" lead capture form
- [ ] Email automation for listing claims (Resend)

### Phase 6: Launch & SEO (Week 8-10) — 5-8h
- [ ] Submit sitemap to Google
- [ ] Verify Search Console indexing
- [ ] Write 10 pillar content pages ("How to choose a dog groomer", etc.)
- [ ] Set up Google Business Profile for the directory itself
- [ ] Social media profiles (Pinterest for pet content)

### Phase 7: Passive Mode (Month 4+) — 1-2h/week
- [ ] Monitor analytics weekly
- [ ] Check for broken data / closed businesses quarterly
- [ ] Add new cities as traffic grows
- [ ] Respond to listing claim requests (automated)

---

## Timeline Summary

| Week | Phase | Hours | Cumulative |
|------|-------|-------|------------|
| 1-2 | Foundation | 20-25h | 20-25h |
| 3 | Data Pipeline | 10-15h | 30-40h |
| 4-5 | SEO Pages | 15-20h | 45-60h |
| 6 | Core Features | 10-15h | 55-75h |
| 7-8 | Monetization | 8-10h | 63-85h |
| 8-10 | Launch & SEO | 5-8h | 68-93h |
| 11+ | Passive Mode | 1-2h/week | Ongoing |

**Total active build: ~70-90 hours over 10 weeks (2-3h/day fits perfectly)**

---

## Database Schema (Core Tables)

```sql
-- Providers (the listings)
providers:
  id, name, slug, category_id,
  address, city, state, zip, lat, lng,
  phone, website, email,
  rating, review_count,
  hours_json, services_json,
  photos_json, description,
  is_claimed, is_featured, featured_until,
  source, source_id,
  created_at, updated_at

-- Categories
categories:
  id, name, slug, icon, description

-- Cities (for SEO pages)
cities:
  id, name, slug, state, state_slug,
  lat, lng, population,
  provider_count

-- Reviews
reviews:
  id, provider_id, author, rating,
  text, source, created_at

-- Claims
claims:
  id, provider_id, email, name,
  status (pending/approved/rejected),
  created_at

-- Featured Payments
featured_payments:
  id, provider_id, stripe_session_id,
  plan (basic/premium), amount,
  starts_at, ends_at, status
```

---

## SEO URL Structure

```
/                                    → Homepage
/[state]                             → State page (e.g., /texas)
/[state]/[city]                      → City page (e.g., /texas/austin)
/[state]/[city]/[category]           → City+Category (e.g., /texas/austin/dog-groomers)
/[state]/[city]/[category]/[slug]    → Individual listing
/blog/[slug]                         → SEO content articles
/claim                               → Claim your listing page
/featured                            → Featured listing upgrade page
```

---

## Key Insights from Greg Isenberg / Frey Chu

1. **Data is the moat** — Anyone can build a directory UI. The hard part is clean, enriched, niche-specific data. That's your competitive advantage.

2. **Scrape Google Maps by exact category** — Don't search "pet services" (too broad). Search "dog groomer", "pet sitter", "veterinary clinic" separately for cleaner data.

3. **Clean aggressively** — Raw data is 50-70% junk. Feed CSVs to Claude Code to remove closed businesses, missing addresses, off-niche entries.

4. **Enrich beyond basics** — The difference between a $0 directory and a $273/day directory is depth: specialties, certifications, photos quality, unique filters. Use Crawl for AI to scan provider websites at scale.

5. **Programmatic SEO is the engine** — Generate hundreds of city+service pages. Each page targets "[service] in [city]" keywords. State pages alone can rank for 1,000+ terms.

6. **Speed to market matters** — Build in days, not months. Claude Code can scaffold the entire stack. First mover advantage in niche directories is real.

7. **Monetize via layers** — Don't pick one revenue model. Stack: AdSense + Featured Listings + Affiliate + Lead Gen. Multiple small streams = resilient revenue.

8. **Directory → SaaS pipeline** — Once you have traffic, build a SaaS layer (booking system, CRM, review management) and sell to the businesses already in your directory. The directory is the acquisition channel.

---

## Files in This Project

```
online_directory_pet/
├── PLAN.md                  ← This file (master plan)
├── CLAUDE.md                ← Project instructions for Claude Code
├── DATABASE.md              ← Full database schema + seed strategy
├── SEO-STRATEGY.md          ← Keyword research + content plan
├── DATA-PIPELINE.md         ← Step-by-step data collection + cleaning
├── MONETIZATION.md          ← Revenue streams + pricing strategy
└── src/                     ← (will be created during Phase 1)
```

---

## Niche Validation Tools

Before building, validate that your niche has real organic traffic potential. In the video, Greg and Frey use these tools to analyze competitor directories (like the funeral home directory) and estimate their traffic/revenue:

| Tool | What It Does | Use It For |
|------|-------------|------------|
| **[Ahrefs](https://ahrefs.com)** | SEO analytics, keyword research, traffic estimation | Find "near me" keywords with 30-100K monthly searches and KD < 20. Spy on competitor directories to see their traffic, top pages, and keywords. This is the primary tool they use in the video to validate niches. |
| **[SimilarWeb](https://similarweb.com)** | Website traffic estimation | Estimate how much traffic a competitor directory gets monthly. Free tier shows basic traffic data. They use this to guess funeral home directory traffic in the video. |
| **[Ubersuggest](https://neilpatel.com/ubersuggest/)** | Keyword research (free alternative to Ahrefs) | Find keyword volume and difficulty. Free tier gives limited daily searches. Good for initial validation before paying for Ahrefs. |
| **[Google Keyword Planner](https://ads.google.com/home/tools/keyword-planner/)** | Official Google keyword volume data | Free with Google Ads account. Shows exact search volumes for your target keywords. Less competitive data than Ahrefs but the volume numbers are from Google itself. |

### How to Validate Our Pet Niche

1. **Go to Ahrefs or SimilarWeb** → search for existing pet directories (Rover.com, DogGroomerDirectory.com, etc.)
2. **Check their organic traffic** → if a basic competitor gets 50K+ visits/mo, the niche has demand
3. **Look at their top pages** → which city/service combinations drive the most traffic?
4. **Search Ahrefs for keywords:**
   - "dog groomer near me" → check volume + KD
   - "vet near me" → check volume + KD
   - "pet sitter [top 10 cities]" → check volume + KD
5. **Compare with the funeral home example from the video** → they showed funeral directories getting significant organic traffic from "near me" searches with low competition. Pet services should be comparable or better given the larger market size ($150B+).

### Geographic Opportunity Mapping (Brazil + USA)

Don't seed data everywhere at once. First, find the **high-demand, low-competition areas** — cities/regions where people are searching for pet services but no specialized directory exists yet. These are your priority launch markets.

**How to find them:**

1. **Ahrefs → Keywords Explorer** — Search "pet groomer [city]", "veterinário [cidade]" for the top 50 cities in both US and Brazil. Export to a spreadsheet with columns: city, keyword, volume, KD, top result.

2. **Google Trends** — Compare search interest for "pet groomer" across US states and Brazilian states. States with rising trends but no niche directory = gold.

3. **Google the keyword yourself** — For each top city, Google "dog groomer in [city]". If the first page shows only Yelp, Google Maps, and generic listings (no dedicated pet directory), that city is wide open.

4. **Score each city:**
   | Factor | Points |
   |--------|--------|
   | Search volume > 1K/mo for "[service] in [city]" | +3 |
   | No niche pet directory in top 10 results | +3 |
   | Only generic results (Yelp, Google Maps, Yellow Pages) | +2 |
   | Growing population / pet-friendly city | +1 |
   | High median income (more spending on pet services) | +1 |

5. **Rank cities by score** — The top 20-30 become your Phase 1 launch markets. Seed data ONLY for these cities first. Expand to lower-scored cities in Phase 2 after SEO gains traction.

**Why this matters:** Curating data for 20 high-opportunity cities beats spreading thin across 200 cities. You rank faster with deeper data per city (more listings, more pages, more internal links) than with shallow data across many cities.

**Example priority cities (to validate):**

| 🇺🇸 US (likely high-opportunity) | 🇧🇷 Brazil (likely high-opportunity) |
|---|---|
| Austin, TX | São Paulo, SP |
| Nashville, TN | Curitiba, PR |
| Denver, CO | Belo Horizonte, MG |
| Portland, OR | Florianópolis, SC |
| Raleigh, NC | Brasília, DF |
| Charlotte, NC | Porto Alegre, RS |
| Tampa, FL | Campinas, SP |
| Boise, ID | Goiânia, GO |

*These are starting guesses — actual priority should come from keyword research data.*

### Quick Validation Checklist
- [ ] "dog groomer near me" has 100K+ monthly searches ✅
- [ ] Keyword difficulty < 20 ✅
- [ ] No single dominant niche directory (Yelp is generic, not specialized) ✅
- [ ] Google results show outdated/basic directories ✅
- [ ] Reddit/social media shows people asking "where to find a good [pet service]" ✅

---

## Next Steps

1. **Validate the niche** using Ahrefs/SimilarWeb (compare with funeral home directory from the video)
2. **Decide target market** — US, Brazil, or both
3. **Run keyword research** to confirm search volumes for your chosen market
4. **Start Phase 1** — set up Next.js + Supabase + base components
5. **Run data pipeline** — scrape, clean, enrich listings
6. **Deploy and submit to Google** — start the SEO clock ticking
