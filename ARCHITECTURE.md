# StellarAdvisor Architecture

## Overview

StellarAdvisor is a lead generation and matching platform connecting Amazon sellers with vetted agency partners.

## System Components

### 1. Seller Portal (Public)
- **URL:** stellaradvisor.com
- **Purpose:** Attract sellers, capture leads, qualify them
- **Tools:**
  - FBA Deal Calculator
  - Agency Match Quiz
  - Category Research (planned)
  - Free Business Audit (planned)

### 2. Partner Portal (Future)
- **URL:** partners.stellaradvisor.com
- **Purpose:** Agency partners manage leads
- **Features:**
  - Lead dashboard
  - Seller profiles
  - Performance analytics

### 3. Admin Portal (Future)
- **URL:** admin.stellaradvisor.com
- **Purpose:** Platform management
- **Features:**
  - Lead routing
  - Partner management
  - Commission tracking

## Data Model

```
SELLERS                 MATCHES                 PARTNERS
─────────               ─────────               ─────────
seller_id (PK)    ───┐  match_id (PK)     ┌─── partner_id (PK)
email                │  seller_id (FK) ───┘    company_name
company_name         │  partner_id (FK)        contact_email
revenue_range        └─ match_score            tier
marketplace             status                 specialties[]
category                commission_due         marketplace[]
pain_points[]           closed_date            commission_rate
lead_score              deal_value             active
source
created_at
```

## Lead Scoring Algorithm

### Seller Score (0-100 points)

| Factor | Points | Criteria |
|--------|--------|----------|
| Revenue | 30 max | $1M+ = 30, $500K-1M = 25, $100K-500K = 15, <$100K = 5 |
| Urgency | 20 max | Immediate = 20, 30 days = 15, 90 days = 10, Exploring = 5 |
| Engagement | 20 max | Quiz complete = 10, Tools used = 5, Docs downloaded = 5 |
| Qualification | 30 max | Email verified = 5, Phone = 10, Brand registered = 10, Call booked = 5 |

### Partner Matching Score

| Factor | Weight | Description |
|--------|--------|-------------|
| Revenue Fit | 40% | Seller revenue within partner's range |
| Marketplace | 25% | Platform overlap (Amazon, Walmart, etc.) |
| Category | 20% | Partner expertise in seller's category |
| Service Fit | 15% | Pain points match partner services |

## Technology Stack

### Current (Static Site)
- HTML/CSS/JavaScript
- No build process required
- Host anywhere (Vercel, Netlify, GitHub Pages)

### Future (Full Platform)
- **Frontend:** Next.js + Tailwind CSS
- **Backend:** Supabase (PostgreSQL + Auth)
- **Forms:** Tally.so or native
- **Email:** Resend or SendGrid
- **Payments:** Stripe
- **APIs:** Rainforest (Amazon data), Keepa

## Integration Points

### Seller Directories (ThreeColts)
- 500K+ verified seller contacts
- Enrichment data for matched leads
- Tiered access for partners

### External APIs
- Rainforest API: Live ASIN data
- Keepa: Historical pricing
- ZeroBounce: Email verification

## Deployment

### Production
- Vercel (recommended)
- Auto-deploys from GitHub main branch
- Custom domain: stellaradvisor.com

### Staging
- Vercel preview deployments
- Every PR gets unique URL

---

*Document maintained by Ryan - Partnerships Manager*
