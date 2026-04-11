# Skills Roadmap

Expansion and improvement plan for webdesign-agency-skills. Ordered by impact on the agency sales and delivery workflow.

## Current Skills

| Skill | Purpose |
|-------|---------|
| `/prospect-audit` | Read-only business-language analysis of any website |
| `/improve` | Targeted improvement loop: audit, recommend, fix, verify |
| `/lighthouse-100` | Automated loop to achieve 100/100/100 Lighthouse scores |
| `/performance-audit` | Core Web Vitals deep dive with element-level attribution |
| `/responsive-check` | Cross-breakpoint testing across 8 viewport sizes |

---

## New Skills

### High Impact — Sales & Prospecting

#### `/competitor-compare`

Side-by-side analysis of a prospect vs. 1-2 competitors.

`prospect-audit` looks at one site in isolation. But the sales conversation is always "you vs. them." This skill audits 2-3 URLs, compares scores, screenshots both, and produces a brief like: "Your competitor loads in 1.4s, you load in 4.2s. They show star ratings in Google, you show a plain link."

**What it does:**
- Takes 2-3 URLs (prospect + competitors)
- Runs lightweight audit on each (performance, mobile, SEO basics, design quality)
- Screenshots each site at desktop + mobile
- Compares scores in a table
- Highlights where the prospect loses and where they win
- Outputs a client-ready comparison brief

**Why it matters:** Concrete competitive data closes deals. Generic "your site needs work" doesn't.

---

#### `/site-crawl`

Multi-page audit across key pages of a site.

All 5 current skills work on a single URL. Agencies audit whole sites. This skill discovers key pages (homepage, about, services, contact), runs `prospect-audit` on each, then synthesizes findings.

**What it does:**
- Takes a domain, discovers key pages (sitemap.xml, nav links, or manual list)
- Runs `prospect-audit` on each page (parallelized)
- Produces per-page scores and a site-wide summary
- Identifies the weakest page: "Your homepage is a 7/10 but your contact page is a 3/10 — that's where you're losing leads"
- Flags cross-page inconsistencies (different fonts, broken nav on subpages, missing footer links)

**Why it matters:** A single-page audit misses site-wide problems. The contact page or pricing page is often where conversions die, and nobody audits it.

---

#### `/quote-generator`

Turn audit findings into a scoped proposal.

After `prospect-audit`, the agency manually translates findings into a quote. This skill takes audit output, maps each finding to a deliverable with effort estimate and price range (configurable), and outputs a structured proposal draft.

**What it does:**
- Takes a `prospect-audit` output file as input
- Maps each finding to a deliverable (e.g., "Fix broken animations" → "Animation repair", quick win, CHF X)
- Groups deliverables into packages (e.g., "Quick Wins Package", "Full Redesign")
- Outputs a proposal draft with scope, timeline, and pricing placeholders
- Configurable via a `.quote-config.md` file (hourly rate, package templates, currency)

**Why it matters:** Closes the gap between "here's what's wrong" and "here's what it costs to fix." Reduces proposal writing time from hours to minutes.

---

### High Impact — Delivery & QA

#### `/conversion-audit`

CTA effectiveness, trust signals, form friction, and funnel analysis.

Current skills cover design quality, performance, accessibility, and responsiveness — but not whether the site actually converts. This is the business-impact layer that `prospect-audit` frames in its brief but doesn't deeply measure.

**What it checks:**
- CTA visibility: Is the primary CTA above the fold? Contrasting color? Clear action verb?
- Trust signals: Reviews, testimonials, logos, certifications, security badges
- Contact friction: How many clicks to reach contact? Is the phone number clickable on mobile? Form length?
- Social proof: Any evidence of real customers?
- Value proposition: Is it clear within 5 seconds what the business does and why you should care?
- Navigation clarity: Can a first-time visitor find what they need?
- Mobile conversion path: Can someone complete the key action on a phone?

**Output:** Scored conversion readiness (1-10) with specific, prioritized fixes framed as lost revenue.

**Why it matters:** A beautiful, fast, accessible site that doesn't convert is a failure. This fills the biggest gap in the current skill set.

---

#### `/before-after`

Visual comparison report after fixes are applied.

After running `/improve` or `/lighthouse-100`, there's no structured way to show the client what changed. This generates a visual diff report ready to send as a deliverable.

**What it does:**
- Takes before/after screenshots (from `clients/<domain>/` directory)
- Takes before/after metrics (Lighthouse scores, Core Web Vitals, audit findings)
- Generates a visual comparison report: side-by-side images, score deltas, specific fixes listed
- Outputs in Markdown (and optionally HTML for email/PDF)

**Output format:**
```
## What We Fixed — [domain]

### Performance
Before: 54 → After: 92 (+38)

### Accessibility
Before: 71 → After: 100 (+29)

### Fixes Applied
1. Compressed hero image (2.4MB → 180KB) — LCP improved by 2.1s
2. Added alt text to 7 images — accessibility score +15
3. Fixed heading hierarchy — SEO score +8

### Visual Comparison
[Desktop before] → [Desktop after]
[Mobile before] → [Mobile after]
```

**Why it matters:** Clients need to see what they paid for. This turns invisible technical work into a tangible deliverable that justifies the invoice and builds trust for future work.

---

### Medium Impact — Expanding the Toolkit

#### `/content-audit`

Copy quality, readability, and messaging clarity analysis.

Separate from design quality: evaluates whether the words on the page actually work. Pairs with Impeccable's `/clarify` command but goes deeper into content strategy.

**What it checks:**
- Headline clarity: Does the H1 communicate what the business does?
- Value proposition: Is it in the first sentence or buried in paragraph 3?
- Reading level: Appropriate for the target audience?
- Wall of text: Paragraphs over 4 lines without breaks?
- Jargon: Industry terms that confuse visitors?
- CTA copy: Generic ("Submit", "Click here") vs. specific ("Get your free quote")?
- Consistency: Does the tone match across pages?
- Missing content: No testimonials? No pricing? No FAQ?

**Output:** Content quality score with specific rewrites suggested for the worst offenders.

**Why it matters:** Many sites have decent design but terrible copy. "We provide innovative solutions for your business needs" is on thousands of sites and converts nobody.

---

#### `/schema-check`

Structured data validation and generation.

Lighthouse catches missing schema but doesn't help build it. This skill validates existing schema, identifies what's missing for the business type, and generates the JSON-LD.

**What it does:**
- Extracts all existing structured data (JSON-LD, Microdata, RDFa)
- Validates against Schema.org specs
- Identifies what's missing based on business type:
  - Local business → LocalBusiness, OpeningHours, GeoCoordinates
  - E-commerce → Product, Offer, AggregateRating
  - Service business → Service, PriceSpecification, AreaServed
  - Any site → Organization, WebSite, BreadcrumbList, FAQ
- Generates complete JSON-LD blocks ready to paste
- Tests with Google Rich Results validator (if available)

**Why it matters:** Schema directly affects how a site appears in Google (star ratings, business hours, FAQ dropdowns, price ranges). Most small business sites have zero structured data. Easy win with visible results.

---

## Improvements to Existing Skills

### `prospect-audit`: Automatic competitor context

Currently the "competitive context" section frames findings against generic industry norms. Enhancement: add an optional `--compare domain2.com` flag that runs a lightweight audit on the competitor and weaves real data into the brief.

Instead of: "Most sites in your space load in under 2 seconds"
Produces: "meier-gartenbau.ch loads in 1.4 seconds. You load in 4.2 seconds."

Implementation: When `--compare` is provided, run a parallel lightweight audit (Lighthouse scores + screenshot only) on the competitor, then inject specific comparisons into the brief template.

---

### `lighthouse-100`: Progress reporting

When fixing 15+ issues across multiple re-runs, the current output is a final summary. Enhancement: add intermediate progress reporting.

```
Round 1: A11y 78 → 91, BP 85 → 100, SEO 82 → 91 (fixed 8 issues)
Round 2: A11y 91 → 100, SEO 91 → 97 (fixed 3 issues)
Round 3: SEO 97 → 100 (fixed 1 issue)

Total: 12 issues fixed in 3 rounds
```

Clients love seeing the journey, not just the destination.

---

## Build Priority

If building three skills to maximize the value of the pack:

| Priority | Skill | Reason |
|----------|-------|--------|
| 1 | `/competitor-compare` | Biggest sales differentiator — competitive data closes deals |
| 2 | `/conversion-audit` | Fills the most obvious gap — design quality ≠ conversions |
| 3 | `/site-crawl` | Makes every other skill work at the site level instead of page level |

After those three, `/before-after` and `/quote-generator` complete the agency workflow from prospecting through delivery to invoicing.
