# Monetization Strategy

## Revenue Streams (Layered)

### Stream 1: Display Ads — $100-500/mo
**When:** Month 3 (need some traffic first)
**How:**
- Google AdSense initially (no minimum traffic)
- Upgrade to Mediavine at 50K sessions/mo ($15-25 RPM)
- Pet niche has high RPM ($8-12 on AdSense, $15-25 on Mediavine)

**Placement:**
- Banner below listing cards (not intrusive)
- Sidebar on desktop
- Between listings on mobile
- In-content on blog posts

**Revenue math:**
| Traffic | RPM | Monthly |
|---------|-----|---------|
| 5K visits | $10 | $50 |
| 10K visits | $10 | $100 |
| 30K visits | $10 | $300 |
| 50K visits | $20 (Mediavine) | $1,000 |

### Stream 2: Featured Listings — $300-500/mo
**When:** Month 4 (need providers to discover their free listings first)
**How:**
- Every provider has a FREE listing (seeded from Google Maps)
- Providers find their listing via Google → see "Claim & Upgrade" CTA
- Paid tiers:

| Plan | Price | Features |
|------|-------|----------|
| Free | $0 | Basic listing: name, address, phone, rating |
| Featured | $99/yr | Verified badge, top of category, 5 photos, services list, description |
| Premium | $199/yr | Everything in Featured + "Featured Provider" badge on city page, priority in search, link to booking |

**Revenue math:**
- Month 4-6: 20-30 providers upgrade = $165-$497/mo
- Month 12: 50-100 providers = $412-$1,658/mo

**Key UX flow:**
1. Provider Googles their business name
2. Finds their listing on our directory
3. Sees "Is this your business? Claim it for free"
4. Claims with email verification
5. Sees upgrade options with clear value prop
6. Pays via Stripe checkout

### Stream 3: Affiliate Revenue — $150-300/mo
**When:** Month 3
**Programs:**

| Program | Commission | Placement |
|---------|-----------|-----------|
| Lemonade Pet Insurance | $25-50/signup | "Protect your pet" CTA on listing pages |
| Trupanion | $25/lead | Sidebar widget on vet pages |
| Chewy | 4-8% per sale | "Shop pet supplies" section |
| Amazon Pet Products | 3-4% per sale | Product recommendations in blog |
| Rover (pet sitting) | $20/first booking | "Book online" alternative on sitter pages |
| BarkBox | $10-15/signup | Blog content + sidebar |

**Placement strategy:**
- Listing pages: pet insurance CTA in sidebar
- Blog posts: product recommendations with affiliate links
- Category pages: "Shop online" section with Chewy/Amazon links
- Individual listings without booking: "Book via Rover" fallback

### Stream 4: Lead Generation — $200-500/mo
**When:** Month 5
**How:**
- "Get a Quote" button on listing pages
- User fills: name, email, service needed, pet type, date
- Lead sent to provider via email + SMS
- Charge provider $5-10 per qualified lead

**Revenue math:**
- 50 leads/mo × $7 avg = $350/mo
- Grows with traffic

### Stream 5 (Future): SaaS Layer — $1K+/mo
**When:** Month 8+ (when you have 50K+ visits/mo)
**What:**
- Online booking system for pet services ($29-49/mo per business)
- Review management dashboard ($19/mo)
- Client CRM for pet businesses ($19-39/mo)
- The directory is the acquisition channel — businesses are already there

---

## Total Revenue Projection

| Month | Ads | Featured | Affiliate | Leads | Total |
|-------|-----|----------|-----------|-------|-------|
| 3 | $50 | $0 | $50 | $0 | $100 |
| 4 | $80 | $100 | $100 | $0 | $280 |
| 5 | $120 | $200 | $150 | $100 | $570 |
| 6 | $150 | $300 | $200 | $200 | $850 |
| 9 | $300 | $400 | $250 | $300 | $1,250 |
| 12 | $500 | $500 | $300 | $400 | $1,700 |

**Conservative estimate:** $500/mo by month 5-6, $1,500+/mo by month 12.

---

## Pricing Page Copy

### Free Listing
"Your business is already listed — claim it to verify your info."
- Basic details shown
- No photos beyond Google Maps
- No verified badge

### Featured — $99/year ($8.25/mo)
"Stand out from the competition."
- ✅ Verified badge
- ✅ Top of category results
- ✅ Up to 5 photos
- ✅ Services list
- ✅ Custom description
- ✅ Direct website link

### Premium — $199/year ($16.58/mo)
"Maximum visibility for your business."
- ✅ Everything in Featured
- ✅ "Featured Provider" badge on city page
- ✅ Priority in all search results
- ✅ Booking link integration
- ✅ Monthly analytics report
- ✅ Highlighted in email newsletter

---

## Payment Flow (Stripe)

1. Provider clicks "Upgrade" on their claimed listing
2. Selects plan (Featured $99/yr or Premium $199/yr)
3. Stripe Checkout session created
4. Payment processed
5. Webhook updates `featured_payments` table
6. Provider listing immediately shows featured/premium badges
7. Auto-renewal with Stripe subscription
8. 30-day money-back guarantee
