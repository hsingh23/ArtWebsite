# ADR 005 — Accept template placeholder content as tracked debt

- Date: 2025-05-07 (recognized) / 2026-09-08 (recorded)
- Status: Accepted as debt
- Commits: `4c4cce5` (introduced), `ce06ea8` (partially corrected)

## Context

Because the site was AI/template-generated, its first published version mixed
genuine customizations with untouched template defaults: `mobiri.se` links
(nav Home/Portfolio, CTA buttons, social icons, footer), lorem-ipsum intro,
"Intro with video" heading, template phone (+1 555 123 4567) and address,
stock partner logos, template testimonials (Eleanor Hughes/Daniel Carter/
Sophia White), and a mixed identity — hero "Rossi Art", navbar "Painting in
Bali", about-persona "Antonio Rossi from Chicago", while the domain and
contact email say paintinginbali.com.

Only the stats were corrected on day one (`ce06ea8`: 7→2 years, 300+→30+
works sold), because inflated numbers were the one actively misleading
element.

## Decision

Ship with placeholders rather than block launch on perfect copy. Treat every
placeholder as a known debt item (this ADR is the register), to be replaced
incrementally through the Mobirise builder (per ADR 003).

## Consequences

- **Positive:** the site existed and was reachable on its custom domain the
  same day it was started.
- **Positive:** correcting the stats showed the template for what it was —
  visitors reading "2 years active" alongside template testimonials likely
  discount the rest of the filler.
- **Negative:** dead `mobiri.se` links on primary buttons ("View Work",
  "Get Started", "Get Quote") are the worst offenders — they look clickable
  and go nowhere useful.
- **Negative:** the identity mismatch (Rossi/Chicago persona vs Bali domain)
  is confusing to real visitors and undermines trust more than lorem ipsum.
- Payoff order if resumed: (1) button/nav links, (2) identity and about copy,
  (3) contact details, (4) testimonials/partners/news, (5) intro-video copy.
