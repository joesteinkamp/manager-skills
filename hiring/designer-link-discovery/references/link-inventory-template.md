# Link Inventory Template

Use this as the default response structure for `designer-link-discovery`.
Every link must carry a confidence rating and a one-line note. Omit any
category that yielded no links, but still record it in `Coverage Summary`.

## Discovery Context

- Candidate:
- Design discipline: (product / UX / visual / brand / motion / design systems)
- Current role & company:
- Location:
- LinkedIn profile: (URL or vanity slug)
- Source of starting details: (active browser tab / user-pasted)
- Disambiguating signals used: (employer, city, handle, etc.)
- Date of search:

## Link Inventory

Grouped by category. Each entry: **URL — confidence — one-line note**.
Confidence is `Confirmed` or `Probable` (put `Unverified` links in the next
section). Name the signal behind each rating.

### Portfolio & Personal Sites
- `url` — **Confidence** — note. *Signal:* why this rating.

### Design Communities
- `url` — **Confidence** — note. *Signal:* why this rating.

### Writing & Publishing
- `url` — **Confidence** — note. *Signal:* why this rating.

### Social
- `url` — **Confidence** — note. *Signal:* why this rating.

### Code
- `url` — **Confidence** — note. *Signal:* why this rating.

### Professional & Other
- `url` — **Confidence** — note. *Signal:* why this rating.

## Needs Verification

Plausible matches that could not be tied to this person. For each: the link,
why it is uncertain, and exactly what a human should check.
- `url` — **Unverified** — why uncertain. *To confirm:* what to check.

## Coverage Summary

- Platforms checked, link found: (list)
- Platforms checked, nothing found: (list)
- Platforms not checked and why: (e.g., "Instagram — not relevant for a
  product designer")

## Recommended Next Steps

- Best link for portfolio review: (which URL to send to `$portfolio-reviewer`)
- Open questions for the recruiter or candidate:
- Any Needs Verification items worth resolving before the screen:

---

## Starter Example

A completed inventory for an illustrative candidate. Use as a quality reference.

### Discovery Context

- Candidate: Jordan Avery
- Design discipline: Product designer (fintech)
- Current role & company: Senior Product Designer, NorthBank
- Location: Austin, TX
- LinkedIn profile: linkedin.com/in/jordanavery-design
- Source of starting details: active browser tab
- Disambiguating signals used: employer "NorthBank", Austin TX, handle
  "@jordandraws"
- Date of search: 2026-05-22

### Link Inventory

#### Portfolio & Personal Sites
- `jordanavery.design` — **Confirmed** — Portfolio, 5 fintech case studies,
  last updated 2025; footer links to Dribbble, X, and GitHub. *Signal:* listed
  in LinkedIn Contact Info.

#### Design Communities
- `dribbble.com/jordandraws` — **Confirmed** — Active Dribbble, ~40 shots,
  mostly mobile banking UI; bio links jordanavery.design. *Signal:* reused
  handle + portfolio cross-link.
- `behance.net/jordandraws` — **Probable** — Behance with 3 older projects,
  inactive since 2022. *Signal:* reused handle; bio names "fintech designer"
  but no explicit cross-link.

#### Writing & Publishing
- `medium.com/@jordandraws` — **Confirmed** — 6 articles on fintech UX and
  design systems; author bio links LinkedIn. *Signal:* explicit cross-link to
  LinkedIn.

#### Social
- `x.com/jordandraws` — **Confirmed** — Active; bio reads "Product designer
  @NorthBank" and links the portfolio. *Signal:* names current employer +
  portfolio cross-link.

#### Code
- `github.com/jordandraws` — **Probable** — Sparse; one design-tokens repo,
  profile README links the portfolio. *Signal:* reused handle + portfolio link,
  but low activity.

### Needs Verification

- `instagram.com/jordan.avery` — **Unverified** — Name matches and account is
  in Austin, but no design content and no cross-link. *To confirm:* check
  whether the candidate lists Instagram anywhere, or ask the recruiter.

### Coverage Summary

- Platforms checked, link found: portfolio domain, Dribbble, Behance, Medium,
  X, GitHub
- Platforms checked, nothing found: Figma Community, Substack, Bluesky, Layers,
  Polywork, Read.cv/Posts
- Platforms not checked and why: Vimeo / YouTube — not relevant for a product
  designer with no motion work

### Recommended Next Steps

- Best link for portfolio review: `jordanavery.design` — send to
  `$portfolio-reviewer`.
- Open questions: Behance work is 4 years old — confirm it is the same person
  before citing it.
- Needs Verification: the Instagram account is low-value; safe to skip unless
  the recruiter wants it confirmed.
