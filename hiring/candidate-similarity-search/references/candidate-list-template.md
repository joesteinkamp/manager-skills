# Candidate List Template

Default response structure for `candidate-similarity-search`. Every
candidate must carry a confidence rating, name the matching attributes,
and link to the source query that surfaced them. Omit any section that
yielded no content, but still record it in `Coverage Summary`.

## Seed Snapshot

- Candidate name:
- Current role & company:
- Location:
- LinkedIn profile: (URL or vanity slug)
- Source of starting details: (active browser tab / user-pasted)
- Date of search:

## Attribute Profile

Grouped by category. Each attribute followed by the profile text it came
from. Mark anything not visible as "not stated".

- **Role:** current title; prior titles; trajectory.
- **Seniority:** years in field; level keyword; IC vs management.
- **Company:** current employer; prior employers; company type; industry.
- **Skills & tools:** top skills; tools / frameworks; methodologies.
- **Domain expertise:** industries; problem types.
- **Education:** degree, school, field.
- **Location:** city; remote signal.
- **Tenure pattern:** avg years per role; total years.
- **Side signals:** open source, writing, speaking.

**Similarity axis used for this search:** (the attributes the user
weighted as must-match; default if the user did not specify.)

## Search Playbook

Grouped by source. Each query labelled with the attributes it targets.

### Google `site:linkedin.com/in/`
- `query` — *targets:* attributes.

### LinkedIn search URLs (require user's login)
- `url` — *targets:* attributes. *Note:* requires LinkedIn login;
  company / industry IDs may need a one-time lookup.

### General web / portfolio
- `query or url` — *targets:* attributes.

## Candidates Found

Ranked by confidence, then by attribute overlap. Each entry:
**Name — profile URL — confidence — matching attributes — source query.**

### Strong matches
- **Name** — `profile-url` — **Strong** — *Matching:* attribute list.
  *Source:* which query surfaced them. One-line note (current role &
  why they're worth a look).

### Possible matches
- **Name** — `profile-url` — **Possible** — *Matching:* attribute list.
  *Source:* which query. One-line note.

### Weak matches (overflow)
- **Name** — `profile-url` — **Weak** — *Matching:* attribute list.
  *Source:* which query. One-line note. *To upgrade:* what would need
  to be true.

## Coverage Summary

- Queries executed in this session: (list)
- Queries left for the user to run (LinkedIn URLs, anything the
  environment couldn't reach):
- Sources checked, nothing relevant found: (list)
- Sources not checked and why: (e.g. "Dribbble — seed is a backend
  engineer, not relevant")

## Recommended Next Steps

- Top 3 candidates to screen first and why.
- Suggested next skill: usually `$de-linkedin-profile-evaluation` on the
  Strong matches before outreach.
- Refinements to suggest if the list is too narrow or too broad (loosen
  the must-match attributes, swap industry for company-type, etc.).
- Open questions for the recruiter (e.g. "Should we accept candidates
  outside <city>?").

---

## Starter Example

A completed list for an illustrative seed. Use as a quality reference.

### Seed Snapshot

- Candidate name: Priya Natarajan
- Current role & company: Staff Product Designer, NorthBank
- Location: Brooklyn, NY
- LinkedIn profile: linkedin.com/in/priyanatarajan-design
- Source of starting details: active browser tab
- Date of search: 2026-05-23

### Attribute Profile

- **Role:** Staff Product Designer (current); Senior Product Designer at
  PayLeap (2021–2023); Product Designer at Mint (2018–2021). Trajectory:
  IC track, no management.
- **Seniority:** ~8 years; Staff-level; IC.
- **Company:** NorthBank (Series C fintech); PayLeap (Series B fintech);
  Mint (consumer fintech, pre-acquisition). All fintech.
- **Skills & tools:** Figma, design systems, prototyping, accessibility,
  user research. Top-2 for sourcing: design systems + Figma.
- **Domain expertise:** Fintech (B2C banking, payments, onboarding).
- **Education:** BFA, RISD (2018).
- **Location:** Brooklyn, NY. No remote signal.
- **Tenure pattern:** 2–3 years per role; 8 years total.
- **Side signals:** Speaker at Config 2024; small Dribbble presence.

**Similarity axis used for this search:** title (Staff Product Designer
or close synonym) + seniority (~7–10 yrs) + design-systems skill +
fintech industry. Defaulted because the user did not specify; happy to
re-run with a different axis.

### Search Playbook

#### Google `site:linkedin.com/in/`
- `site:linkedin.com/in/ "Staff Product Designer" "fintech" "New York"`
  — *targets:* title + industry + city.
- `site:linkedin.com/in/ "design systems" "Figma" "fintech"` —
  *targets:* top-2 skills + industry.
- `site:linkedin.com/in/ "Senior Product Designer" "fintech" -"NorthBank"`
  — *targets:* one level down + industry, peers elsewhere.
- `site:linkedin.com/in/ "RISD" "product designer"` — *targets:* alumni
  + discipline.

#### LinkedIn search URLs (require user's login)
- `https://www.linkedin.com/search/results/people/?keywords=Staff%20Product%20Designer%20fintech&geoUrn=%5B%22103644278%22%5D`
  — *targets:* title + industry + NYC. *Note:* geoUrn is the LinkedIn
  geo-ID for the New York metro; replace if scope changes.

#### General web / portfolio
- `site:read.cv "Product Designer" "fintech"` — *targets:* discipline +
  industry on read.cv.
- `site:dribbble.com "product designer" "fintech"` — *targets:*
  discipline + industry on Dribbble.

### Candidates Found

#### Strong matches
- **Devon Marsh** — `linkedin.com/in/devon-marsh-design` — **Strong** —
  *Matching:* title (Staff Product Designer), seniority (~9 yrs), design
  systems, fintech (Series C). *Source:* Google site: query 1. Currently
  at LedgerLine; led their design-systems re-platform — exact profile.
- **Mia Okonkwo** — `linkedin.com/in/miaokonkwo` — **Strong** —
  *Matching:* title, seniority (~8 yrs), Figma + design systems, fintech.
  *Source:* Google site: query 2. NYC-based, design lead at
  Currentwise; ex-Stripe.

#### Possible matches
- **Ari Levin** — `linkedin.com/in/arilevin` — **Possible** —
  *Matching:* seniority (Staff), design systems, fintech; title is
  "Design Systems Lead" not "Product Designer". *Source:* Google site:
  query 2. Strong systems work; less generalist than the seed.

#### Weak matches (overflow)
- **Jordan Avery** — `linkedin.com/in/jordanavery-design` — **Weak** —
  *Matching:* fintech + product designer; junior (~3 yrs). *Source:*
  Google site: query 3. *To upgrade:* would need to be a senior+, or
  the user would need to expand the seniority range.

### Coverage Summary

- Queries executed in this session: all four Google site: queries; both
  general-web queries.
- Queries left for the user to run: the LinkedIn search URL (requires
  the user's login).
- Sources checked, nothing relevant found: Dribbble (no fintech-tagged
  product work surfaced for NYC).
- Sources not checked and why: GitHub — seed shows no code signal;
  Behance — not a strong platform for product designers in fintech.

### Recommended Next Steps

- Screen Devon Marsh and Mia Okonkwo first via
  `$de-linkedin-profile-evaluation`-equivalent for the role.
- Run the LinkedIn search URL in a logged-in tab — it will likely
  surface 10–20 more profiles the public web does not.
- If the list feels too narrow, loosen `fintech` to "financial services
  + payments + crypto" and re-run.
- Open question: is "design systems" still a must-have for this hire,
  or only for the seed? Toggling it will materially change the pool.
