# Pet Services Online Directory

## Project Overview
A niche online directory for pet services (groomers, walkers, sitters, vets, pet shops) built with Next.js + Supabase, monetized via AdSense + featured listings + affiliate.

## Stack
- **Framework:** Next.js 14 (App Router, SSG)
- **Database:** Supabase (PostgreSQL + Auth + Storage)
- **Hosting:** Vercel
- **Payments:** Stripe
- **Email:** Resend
- **Analytics:** GA4 + Google Search Console
- **Data:** Google Maps API, Outscraper, Claude Code for cleaning

## Architecture
- Static Site Generation (SSG) for all directory pages (SEO)
- Supabase for dynamic data (claims, reviews, payments)
- Programmatic page generation: /[state]/[city]/[category]/[listing]
- API routes for: claim submission, contact form, payment webhook

## Commands
- `npm run dev` — local development
- `npm run build` — production build
- `npm run seed` — run data seed script
- `npm run clean-data` — run Claude Code data cleaning pipeline

## Key Directories
- `src/app/` — Next.js pages and layouts
- `src/components/` — Reusable UI components
- `src/lib/` — Database client, utilities, constants
- `scripts/` — Data scraping, cleaning, seeding scripts
- `data/` — Raw and cleaned CSV data files
- `public/` — Static assets, images

## Conventions
- TypeScript throughout
- Tailwind CSS for styling
- Slug format: lowercase-kebab-case
- All pages must include Schema.org LocalBusiness markup
- Every listing page must have a "Claim Your Listing" CTA
