---
name: compare
description: "Compare two websites side by side — audit scores, design quality, and specific differences"
---

# /compare — Side-by-Side Website Comparison

Audit two URLs in parallel and present a structured comparison: scores, strengths, weaknesses, and a clear recommendation.

## Input

```
/compare [url-a] [url-b]
```

**Use cases:**
- Your site vs. a competitor
- Before vs. after a redesign
- Two design approaches for the same project
- Client's current site vs. your proposed redesign

If fewer than two URLs are provided, ask for the missing one(s). Do not proceed with a single URL.

---

## Phase 0: Load Both

### Context Swap

1. Check for `.impeccable.md` in the project root.
2. If it exists: Impeccable will use it automatically for both sites.
3. If it does NOT exist: ask the user which site (if either) is "theirs." Use that site's design language as context, or run `/teach-impeccable` first.

### Load Targets

1. Launch Playwright and navigate to URL A. Wait for network idle or 5s timeout. Take a **desktop screenshot** (1280px) and a **mobile screenshot** (390px).
2. Navigate to URL B. Same process: desktop + mobile screenshots.
3. If either URL fails to load (404, timeout, SSL error, WAF block, connection refused): report which URL failed and the specific error. **Abort.** Do not proceed with only one site.

You now have four screenshots. Keep them in context for all subsequent phases.

---

## Phase 1: Diagnose Both

Run the diagnostic commands against each site independently. Save all findings -- do not present them yet.

### Site A

1. **`/audit`** on URL A — structural analysis: accessibility, semantic HTML, responsive behavior, performance signals, code quality
2. **`/critique`** on URL A — design analysis: visual hierarchy, typography, color usage, spacing, consistency, emotional impact

### Site B

1. **`/audit`** on URL B — same structural analysis
2. **`/critique`** on URL B — same design analysis

### Additional Signals (both sites)

Collect via Playwright for each site:

| Signal | How |
|--------|-----|
| Page title | `document.title` |
| Meta description | `<meta name="description">` |
| H1 content | First `<h1>` text |
| Font stack | Computed font-family on `body` and `h1` |
| Load time | Navigation timing (domContentLoaded, load event) |
| Console errors | JS errors logged during page load |
| Images without alt | Count of `<img>` with empty or missing `alt` |
| Horizontal overflow | `document.body.scrollWidth > window.innerWidth` |
| Mobile touch targets | Buttons/links smaller than 44x44px |

---

## Phase 2: Compare

Build the comparison from the audit and critique findings. Present it in this exact structure:

```markdown
## Comparison: [domain-a] vs [domain-b]

### Score Comparison

| Metric | [domain-a] | [domain-b] | Winner |
|--------|-----------|-----------|--------|
| Accessibility | X/10 | Y/10 | domain |
| Performance | X.Xs load | Y.Ys load | domain |
| Anti-patterns | count | count | domain |
| Typography | rating | rating | domain |
| Color / contrast | rating | rating | domain |
| Mobile | rating | rating | domain |
| Overall | X/10 | Y/10 | domain |

### Where [domain-a] Wins
- [Specific advantage with measurable detail]
- [Another advantage — reference actual elements, timings, or content]

### Where [domain-b] Wins
- [Specific advantage with measurable detail]
- [Another advantage]

### Key Differences
- [Notable design or technical differences that are neither better nor worse — just different approaches]
- [e.g., "Site A uses a dark theme with sans-serif type; Site B uses light theme with serif headings"]

### Recommendation
[1-2 sentences: which site is stronger overall and why. If genuinely equal, say so.]
```

### Comparison Rules

1. **Be specific, not vague.** "Site A loads in 1.2s vs Site B's 4.8s" -- not "Site A is faster."
2. **Use numbers when available.** Contrast ratios, load times, error counts, image counts.
3. **Do not force a winner.** If a metric is genuinely equal or too close to call, mark it as "Tie" in the Winner column.
4. **Distinguish taste from quality.** Note when a difference is subjective (design style, color preference) vs. objective (contrast ratio, load time, missing alt text). Use "(subjective)" or "(objective)" labels when the distinction matters.
5. **Reference actual content.** Mention specific headings, images, sections, or components by name -- not "the hero section" when you can say "the 'Transform Your Business' hero with the dashboard mockup."
6. **Keep sections balanced.** If one site has five wins and the other has one, that is fine -- but make sure you looked hard enough at the weaker site. Every site does something right.

---

## Phase 3: Actionable Next Steps

Based on the comparison context, offer the appropriate follow-up:

| Context | Offer |
|---------|-------|
| Your site vs. competitor | "Want to run `/improve` to close the gaps identified above?" |
| Before vs. after redesign | Summarize what improved and what regressed since the change |
| Two design approaches | Recommend which to proceed with, referencing specific findings |
| Client site vs. your redesign | Highlight the concrete improvements your version delivers |

If the user's intent is unclear, ask: "Which of these two sites is yours? That helps me tailor the next steps."

---

## Rules

1. **Both sites get equal scrutiny.** Do not audit one thoroughly and skim the other. Same depth, same rigor.
2. **Never modify either site.** This skill is READ-ONLY. No code edits, no file writes (except the comparison output).
3. **Screenshots are mandatory.** The visual comparison is the foundation. Do not skip screenshots because of load issues -- if screenshots fail, the load failed and you should abort per Phase 0.
4. **Present the comparison, then stop.** Do not automatically run `/improve` or any fix commands. Offer them as next steps and wait for the user.
5. **Respect `.impeccable.md`.** Design quality judgments must align with the project's stated aesthetic direction. A minimalist site is not "too empty" if the design context calls for minimalism.
6. **Localization.** If both sites share a language, write the comparison in that language. If they differ, default to English unless the user specifies otherwise.
