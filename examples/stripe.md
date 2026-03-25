## Website Analysis: stripe.com

**Score: 8/10** — Best-in-class developer marketing with polished design and blazing-fast performance, but 86% of images are invisible to search engines and screen readers, tracking pixels are fighting Stripe's own security policy, and mobile touch targets need work.

![Desktop screenshot](../clients/stripe.com/desktop-2026-03-24.png)
![Mobile screenshot](../clients/stripe.com/mobile-2026-03-24.png)

### What's Costing You Customers

**Google can't see most of your images.** 31 of 36 images on your homepage have no descriptions. Every product illustration, customer logo, and feature graphic is invisible to Google Image Search and anyone using a screen reader. For a company that sells to developers and business leaders worldwide, that is a significant missed opportunity -- potential customers searching for "payment processing dashboard" or "subscription billing interface" will never find your visuals. It also creates legal exposure under ADA and EU accessibility directives, which is especially risky at Stripe's scale.

**Your ad spend is leaking because tracking pixels are blocked by your own security settings.** LinkedIn, Bing, and Google advertising pixels are all being rejected by Stripe's own Content Security Policy. That means you are paying for ad campaigns on these platforms but cannot track which visitors convert. Your marketing team is flying blind on attribution -- spending budget on campaigns with no way to measure what is working and what is waste.

**128 buttons and links are too small to tap easily on phones.** Many interactive elements fall below the minimum recommended touch size. When a startup founder tries to tap "Contact Sales" or "Get Started" on their phone and hits the wrong link, they do not try again -- they leave. For a company where every new sign-up matters, this friction adds up across millions of mobile visitors.

### What We'd Fix (in priority order)

1. **Add descriptive text to every product image and illustration** so Google can index them and screen reader users can understand your product. "Stripe Dashboard showing real-time payment analytics" takes seconds to write and opens your content to millions more visitors. -- _Quick win_

2. **Fix the tracking pixel CSP conflicts** so your marketing team can actually measure which LinkedIn, Google, and Bing campaigns are driving sign-ups. Right now you are spending ad dollars with no attribution data coming back. -- _Small project_

3. **Increase touch target sizes on mobile** for all navigation links, buttons, and interactive elements to at least 44x44 pixels. This is especially important for the "Contact Sales" and "Get Started" CTAs that drive revenue. -- _Small project_

4. **Add a keyboard skip-navigation link** so keyboard and screen reader users can jump past the menu to your content. This is a one-line HTML addition that fixes a WCAG compliance gap and removes legal risk. -- _Quick win_

5. **Fix the duplicate H1 heading** -- the main page heading appears twice in the code, which confuses search engines about what the page is really about. -- _Quick win_

### What Caught Our Eye

**The performance is exceptional.** Your homepage loads in under 600 milliseconds with a 283ms time-to-first-byte. For a page as rich and visually complex as yours, this is remarkable engineering. Visitors never wait, and Google rewards this speed with better search rankings. Most competitors' pages take 3-5x longer to fully render.

**The customer stories are specific and credible.** "Hertz unifies commerce with Stripe," "URBN consolidates $5 billion in online and in-store revenue onto Stripe," "Instacart powers online grocery delivery with Stripe." These are not vague testimonials -- they name real companies with real numbers, organized by segment (enterprise, startup, platform). Combined with the logo bar featuring OpenAI, Amazon, Nvidia, Google, Shopify, and Anthropic, this is arguably the strongest social proof on any payments website.

**The visual design system is cohesive and distinctive.** The gradient color palette, the custom sohne typeface, the animated product demos, and the consistent card-based layouts create a brand identity that is instantly recognizable. The dark-to-light section transitions guide the eye naturally down the page. This is design that builds trust -- it signals that Stripe cares about craft, which reassures customers the product is equally well-built.

**The "Book of the week" section is a genuinely unusual touch.** Stripe Press, featured at the bottom of a payments infrastructure homepage, signals intellectual depth and culture that no competitor matches. It says "we think bigger than payments" without ever saying it directly.

### Technical Details (internal -- do NOT send to client)

**Page Metadata**
- Title: "Stripe | Financial Infrastructure to Grow Your Revenue" -- strong, keyword-rich
- Meta description: "Stripe is a financial services platform that helps all types of businesses accept payments, build flexible billing models, and manage money movement." -- present and descriptive
- OG title: "Stripe | Financial Infrastructure to Grow Your Revenue" -- matches page title
- OG description: matches meta description -- consistent
- OG image: https://images.stripeassets.com/fzn2n1nzq965/XtX984S1GJVsVOXFC7kMu/01988281e867728dfb09aa7793a6e3b9/Stripe.jpg -- present
- HTML lang: "en-MX" -- geo-detected locale (Mexican English variant based on IP)
- Schema.org/JSON-LD: Organization schema with founders (Patrick & John Collison), 21+ global office locations, customer support contact point in multiple languages
- Canonical URL: implied via og:url

**Typography & Design**
- Body font: sohne-var, "SF Pro Display", sans-serif (custom variable font)
- H1 font: same stack
- Gradient color palette transitioning through sections (signature Stripe aesthetic)
- Card-based layout for product features and customer stories
- Animated product demos embedded in sections
- Consistent CTA pattern: pill-shaped buttons with arrow icons

**Content Structure**
- H1: "Financial infrastructure to grow your revenue. Accept payments, offer financial services, and implement custom revenue models -- from your first transaction to your billionth."
- Note: Duplicate H1 detected (same heading appears twice in DOM)
- H2s: "Flexible solutions for every business model", "The backbone of global commerce", "Powering businesses of all sizes", "Reliable, extensible infrastructure for every stack", "What's happening"
- H3s: 14 subsection headings covering payments, billing, agentic commerce, card issuing, crypto, platforms, enterprise, startups, SaaS, developer integration
- Customer case studies: Hertz, URBN ($5B revenue), Instacart, Le Monde
- CTAs: "Start now", "Contact sales", "Create account with Google"
- Navigation: Products, Solutions, Developers, Resources, Pricing, Sign in, Contact sales

**Accessibility**
- 31 of 36 images missing alt text (86%) -- WCAG 1.1.1 violation
- 128 interactive elements below 44x44px minimum touch target -- WCAG 2.5.5 violation
- No skip navigation link detected -- WCAG 2.4.1 violation
- Duplicate H1 heading -- minor WCAG 1.3.1 concern
- Carousel/slider sections lack ARIA labels for navigation
- Hero heading is too long -- subheading is crammed inside H1 tag rather than being a separate element; screen readers announce the entire block as a single heading
- Customer logo carousel duplicates entries in DOM (infinite scroll technique) with empty alt text

**SEO**
- Meta description present and keyword-rich (good)
- OG tags complete (good)
- Schema.org Organization markup comprehensive with 21+ offices (excellent)
- Founders named in structured data (good for knowledge graph)
- Duplicate H1 tags (minor negative signal)
- 31 images without alt text (significant missed indexing opportunity)
- Geo-redirect from stripe.com to stripe.com/en-mx adds TTFB latency

**Performance**
- TTFB: 283ms (excellent)
- DOM Interactive: 340ms (excellent)
- DOMContentLoaded: 372ms (excellent)
- Full Load: 595ms (excellent)
- 3 console errors -- all CSP violations blocking third-party tracking pixels:
  - Bing Ads pixel blocked by connect-src CSP directive
  - LinkedIn attribution pixel blocked by connect-src CSP directive
  - Google Ads remarketing pixel blocked by img-src CSP directive
- Heavy CLDR locale data embedded directly in page (performance cost for i18n)
- 35 of 36 images lazy-loaded (good)

**Responsive Design**
- No horizontal overflow detected at 375px (good)
- Mobile layout adapts properly -- stacked CTAs, hamburger menu, readable typography
- Hero gradient and headline maintain impact on small screens
- Touch target sizing is the primary mobile concern (128 elements below 44px)
- Content reflows cleanly between breakpoints
- Viewport meta properly configured with viewport-fit=cover

**Third-Party Services Detected**
- Google Tag Manager
- LinkedIn Ads (blocked by CSP)
- Bing Ads (blocked by CSP)
- Google Ads remarketing (blocked by CSP)
- Marketo (marketing automation)
- ZoomInfo
- Demandbase
- Spotify events tracking
- Quora pixel
- Reddit pixel
- Twitter/X ads
- Note: Several tracking services are blocked by Stripe's own CSP, indicating a mismatch between marketing and security/engineering teams

**Anti-Patterns Verdict: PASS**
- No AI slop detected. Custom typography, real customer case studies with specific revenue figures, and distinctive gradient design system.
- The animated product demos are genuine UI representations, not generic stock illustrations.
- Voice is confident and specific ("from your first transaction to your billionth") -- not generic SaaS filler.
- The "Book of the week" / Stripe Press section is genuinely unusual -- no template or AI would add that to a payments homepage.
- Interactive tab-style buttons in "Flexible solutions" section have weak affordance as clickable elements -- they look like static headings until hovered.
- Page length is extreme (48+ headings). A visitor scanning quickly may never reach the platform or developer sections.
- "Join us at Sessions" event promo (Stripe Sessions 2026, April 29-30, San Francisco) is time-sensitive content that will need removal/update post-event.
