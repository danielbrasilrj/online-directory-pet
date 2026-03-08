# SEO Strategy — Pet Services Directory

## Core Approach: Programmatic SEO

Generate hundreds of location + service pages that target high-volume "near me" keywords. Each page is statically generated (SSG) for fast load times and SEO.

## Target Keywords

### Primary (High Volume)
| Keyword | Monthly Searches | KD | Priority |
|---------|-----------------|-----|----------|
| dog groomer near me | 200K+ | <20 | P0 |
| vet near me | 300K+ | <20 | P0 |
| pet sitter near me | 90K+ | <15 | P0 |
| dog walker near me | 60K+ | <15 | P0 |
| pet shop near me | 150K+ | <20 | P0 |

### Long-tail (City-Specific)
| Pattern | Example | Est. Volume |
|---------|---------|-------------|
| [service] in [city] | dog groomer in austin | 500-2K |
| best [service] [city] | best vet in chicago | 200-1K |
| [service] [city] [state] | pet sitter miami florida | 100-500 |
| affordable [service] [city] | affordable dog groomer brooklyn | 50-200 |
| [service] near [neighborhood] | vet near downtown denver | 50-200 |

### Content Keywords (Blog)
| Topic | Keyword | Volume |
|-------|---------|--------|
| How to choose a dog groomer | how to choose dog groomer | 5K |
| Dog grooming prices | dog grooming prices | 15K |
| How often to groom a dog | how often to groom dog | 8K |
| Pet insurance worth it | is pet insurance worth it | 20K |
| Best pet food brands | best dog food brands | 30K |

## Page Structure

### 1. State Pages (50 pages)
**URL:** `/texas`
**Title:** "Pet Services in Texas — Find Groomers, Vets, Sitters Near You"
**Content:**
- Overview of pet services in the state
- Top cities grid with provider counts
- Category breakdown
- Featured providers
- Schema.org: WebPage + BreadcrumbList

### 2. City Pages (~200 pages, top cities)
**URL:** `/texas/austin`
**Title:** "Pet Services in Austin, TX — Groomers, Vets, Sitters & More"
**Content:**
- Category cards with counts (e.g., "42 Dog Groomers in Austin")
- Map with all providers
- Top-rated providers list
- City description (auto-generated)
- Schema.org: WebPage + BreadcrumbList

### 3. City + Category Pages (~1,600 pages)
**URL:** `/texas/austin/dog-groomers`
**Title:** "Best Dog Groomers in Austin, TX — Rated & Reviewed"
**Content:**
- All groomers in Austin, sorted by rating
- Filter: rating, price range, distance, services
- Each listing card: name, rating, address, phone, top review snippet
- Schema.org: ItemList + BreadcrumbList

### 4. Individual Listing Pages (~20K-40K pages)
**URL:** `/texas/austin/dog-groomers/happy-paws-grooming`
**Title:** "Happy Paws Grooming — Dog Groomer in Austin, TX"
**Content:**
- Full provider details: address, phone, hours, services, photos
- Map embed
- Reviews section
- "Claim This Listing" CTA
- Related providers nearby
- Schema.org: LocalBusiness + BreadcrumbList + AggregateRating

### 5. Blog Posts (10-20 pillar articles)
**URL:** `/blog/how-to-choose-dog-groomer`
**Content:**
- 1,500-2,000 word guide
- Internal links to relevant city+category pages
- Affiliate product recommendations
- Schema.org: Article + BreadcrumbList

## Technical SEO Checklist

- [ ] XML Sitemap with all pages (split into sub-sitemaps if >50K URLs)
- [ ] robots.txt allowing all crawlers
- [ ] Canonical URLs on every page
- [ ] Breadcrumb navigation (Home > State > City > Category > Listing)
- [ ] Schema.org markup (LocalBusiness, BreadcrumbList, AggregateRating)
- [ ] Open Graph tags for social sharing
- [ ] Mobile-first responsive design
- [ ] Core Web Vitals: LCP < 2.5s, CLS < 0.1, INP < 200ms
- [ ] Image optimization (WebP, lazy loading, alt text)
- [ ] Internal linking (related listings, nearby cities, same category)
- [ ] 404 page with search and popular links
- [ ] Google Search Console verified
- [ ] Google Business Profile for the directory itself

## Content Calendar (Month 2-3)

| Week | Content | Target Keyword |
|------|---------|---------------|
| 1 | How to Choose a Dog Groomer | how to choose dog groomer |
| 1 | Dog Grooming Prices Guide | dog grooming prices 2026 |
| 2 | How Often Should You Groom Your Dog | how often groom dog |
| 2 | Best Dog Food Brands | best dog food brands |
| 3 | Is Pet Insurance Worth It | pet insurance worth it |
| 3 | How to Find a Good Vet | how to find good vet |
| 4 | Pet Sitter vs Boarding | pet sitter vs boarding |
| 4 | Dog Walker Cost Guide | dog walker cost |

## Link Building (Passive)

- Submit to directories: DMOZ alternatives, niche pet directories
- Create embeddable badges: "Top Rated on [DirectoryName]" for providers to add to their sites
- Guest posts on pet blogs (link to city pages)
- Pinterest: pin city guides with links back
- Reddit: genuinely helpful answers in r/dogs, r/pets, r/doggrooming with directory link in profile
