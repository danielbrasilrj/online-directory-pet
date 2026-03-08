# Database Schema & Seed Strategy

## Tables

### providers
The core listing table. Each row is one pet service business.

```sql
CREATE TABLE providers (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  slug TEXT UNIQUE NOT NULL,
  category_id UUID REFERENCES categories(id),

  -- Location
  address TEXT,
  city TEXT NOT NULL,
  state TEXT NOT NULL,
  state_slug TEXT NOT NULL,
  zip TEXT,
  lat DECIMAL(10,7),
  lng DECIMAL(10,7),

  -- Contact
  phone TEXT,
  website TEXT,
  email TEXT,

  -- Ratings
  rating DECIMAL(2,1),
  review_count INTEGER DEFAULT 0,

  -- Details
  hours JSONB,          -- {"mon":"9-18","tue":"9-18",...}
  services JSONB,       -- ["grooming","bathing","nail trim"]
  specialties JSONB,    -- ["large dogs","cats","exotic pets"]
  photos JSONB,         -- ["url1","url2",...]
  description TEXT,
  price_range TEXT,     -- "$","$$","$$$"

  -- Directory meta
  is_claimed BOOLEAN DEFAULT false,
  is_featured BOOLEAN DEFAULT false,
  featured_until TIMESTAMPTZ,
  verified BOOLEAN DEFAULT false,

  -- Source tracking
  source TEXT DEFAULT 'google_maps',  -- google_maps, manual, claimed
  source_id TEXT,                      -- Google Place ID

  -- Enrichment
  accepts_large_dogs BOOLEAN,
  cat_specialist BOOLEAN,
  emergency_24h BOOLEAN,
  organic_products BOOLEAN,
  mobile_service BOOLEAN,

  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);

CREATE INDEX idx_providers_city ON providers(state_slug, city);
CREATE INDEX idx_providers_category ON providers(category_id);
CREATE INDEX idx_providers_location ON providers USING gist(
  ll_to_earth(lat, lng)
);
CREATE INDEX idx_providers_featured ON providers(is_featured) WHERE is_featured = true;
```

### categories
Pet service categories for filtering.

```sql
CREATE TABLE categories (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,           -- "Dog Groomers"
  slug TEXT UNIQUE NOT NULL,    -- "dog-groomers"
  name_pt TEXT,                 -- "Tosadores de Cachorro"
  icon TEXT,                    -- SVG icon name
  search_terms JSONB,          -- ["dog groomer","pet grooming","dog grooming salon"]
  description TEXT,
  provider_count INTEGER DEFAULT 0,
  created_at TIMESTAMPTZ DEFAULT now()
);
```

**Seed categories:**
| Name | Slug | Google Maps Search Term |
|------|------|----------------------|
| Dog Groomers | dog-groomers | "dog groomer" |
| Pet Sitters | pet-sitters | "pet sitter" |
| Dog Walkers | dog-walkers | "dog walker" |
| Veterinary Clinics | veterinary-clinics | "veterinary clinic" |
| Pet Shops | pet-shops | "pet shop" |
| Dog Trainers | dog-trainers | "dog trainer" |
| Pet Boarding | pet-boarding | "pet boarding" |
| Emergency Vet | emergency-vet | "emergency vet" |

### cities
Pre-generated for programmatic SEO pages.

```sql
CREATE TABLE cities (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,           -- "Austin"
  slug TEXT NOT NULL,           -- "austin"
  state TEXT NOT NULL,          -- "Texas"
  state_slug TEXT NOT NULL,     -- "texas"
  state_abbr TEXT NOT NULL,     -- "TX"
  lat DECIMAL(10,7),
  lng DECIMAL(10,7),
  population INTEGER,
  provider_count INTEGER DEFAULT 0,
  UNIQUE(slug, state_slug)
);
```

### reviews
Imported from Google Maps + user-submitted.

```sql
CREATE TABLE reviews (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  provider_id UUID REFERENCES providers(id) ON DELETE CASCADE,
  author TEXT,
  rating INTEGER CHECK (rating BETWEEN 1 AND 5),
  text TEXT,
  source TEXT DEFAULT 'google',  -- google, user
  created_at TIMESTAMPTZ DEFAULT now()
);
```

### claims
When a business owner claims their listing.

```sql
CREATE TABLE claims (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  provider_id UUID REFERENCES providers(id),
  name TEXT NOT NULL,
  email TEXT NOT NULL,
  phone TEXT,
  message TEXT,
  status TEXT DEFAULT 'pending' CHECK (status IN ('pending','approved','rejected')),
  created_at TIMESTAMPTZ DEFAULT now()
);
```

### featured_payments
Stripe payments for featured listings.

```sql
CREATE TABLE featured_payments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  provider_id UUID REFERENCES providers(id),
  stripe_session_id TEXT,
  stripe_customer_id TEXT,
  plan TEXT CHECK (plan IN ('basic','premium')),
  amount INTEGER,            -- cents
  starts_at TIMESTAMPTZ,
  ends_at TIMESTAMPTZ,
  status TEXT DEFAULT 'active',
  created_at TIMESTAMPTZ DEFAULT now()
);
```

## Seed Strategy

### Step 1: Google Maps Bulk Export
Use Outscraper or Google Maps API to export:
- 8 categories × 50 cities = 400 searches
- Expected raw data: 50K-100K rows
- Cost: ~$50-100 via Outscraper

### Step 2: Claude Code Cleaning Prompt
```
Clean this CSV of pet service providers:
1. Remove rows with no name OR no address OR no city OR no state
2. Remove permanently closed businesses (status = "CLOSED_PERMANENTLY")
3. Remove off-niche businesses: Walmart, Target, PetSmart (keep only independent/small businesses)
4. Deduplicate by phone number (keep highest rated)
5. Deduplicate by exact address match
6. Normalize state names to full names (CA → California)
7. Generate slugs from name + city (e.g., "happy-paws-grooming-austin")
8. Output clean CSV with columns: name, slug, category, address, city, state, state_slug, zip, lat, lng, phone, website, rating, review_count, hours_json, source_id
```

### Step 3: Enrichment (Crawl for AI)
For top 5K listings (highest rated):
- Crawl their websites
- Extract: services list, specialties, pricing indicators, certifications
- Use Claude Vision on photos for quality scoring
- Add enrichment columns to database

### Step 4: Supabase Import
```bash
# Import cleaned CSV to Supabase
npx supabase db seed --file data/providers-clean.csv
```
