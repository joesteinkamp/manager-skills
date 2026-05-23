# Search Playbook

Query patterns for finding similar candidates, plus the confidence model
and disambiguation rules. Use `attribute-extraction.md` for *what* to pull
from the seed; use this file for *how* to search and *how confident* to
be in a match.

## Source 1 — Google `site:linkedin.com/in/`

These work in any browser without a LinkedIn login. They surface public
LinkedIn profiles that match keyword patterns. Always wrap multi-word
phrases in quotes.

**Title + industry + location**
- `site:linkedin.com/in/ "<title>" "<industry>" "<city>"`
- `site:linkedin.com/in/ "Senior Product Designer" "fintech" "New York"`

**Title at peer companies (exclude the seed's employer)**
- `site:linkedin.com/in/ "<title>" "<peer-company>"`
- `site:linkedin.com/in/ "<title>" -"<seed-company>"`

**Skills-led search (when the user weights skills above title)**
- `site:linkedin.com/in/ "<skill 1>" "<skill 2>" "<city>"`
- `site:linkedin.com/in/ "design systems" "Figma" "<city>"`

**Alumni-of patterns**
- `site:linkedin.com/in/ "<school>" "<title>"`
- `site:linkedin.com/in/ "<prior-employer>" "<title>"` (people who held
  the seed's prior role at the seed's prior company)

**Seniority filters**
- Combine with the level keyword: `"Staff Engineer"`, `"Principal
  Designer"`, `"Head of Growth"`.

Label each query in the playbook with the attributes it targets, for
example: `[title + industry + city]`.

## Source 2 — LinkedIn search URLs

Prebuilt URLs the user opens in their own logged-in LinkedIn session. The
skill cannot execute these itself, but it can construct them so the user
just clicks.

**People search base**
- `https://www.linkedin.com/search/results/people/?keywords=<URL-encoded-keywords>`

**With filters** (add as query params):
- `&geoUrn=%5B%22<geoId>%22%5D` — location filter; `geoId` comes from a
  one-time lookup the user does on LinkedIn (or surface the city in
  `keywords` instead).
- `&currentCompany=%5B%22<companyId>%22%5D` — filter by current company.
- `&pastCompany=%5B%22<companyId>%22%5D` — filter by past company.
- `&title=<URL-encoded-title>` — filter by current title.
- `&industry=%5B%22<industryId>%22%5D` — industry filter.

Note in the output that these URLs require a LinkedIn login and that
company / industry IDs require a one-time lookup. When IDs are unknown,
fall back to a keyword-only URL the user can refine in-app.

**Recruiter-specific URLs** — if the user has LinkedIn Recruiter, point
them at `linkedin.com/talent/search` with the same filter logic. Do not
assume Recruiter access; offer it as an upgrade path.

## Source 3 — general web and portfolio platforms

Useful for finding similar people whose strongest signals live off
LinkedIn — engineers on GitHub, designers on Dribbble / Behance / Read.cv,
writers on Medium / Substack.

**Platform-scoped search**
- `site:github.com "<seed-skill>" "<city>"` (engineer sourcing)
- `site:dribbble.com "<seed-title>" "<city>"`
- `site:read.cv "<seed-title>" "<industry>"`
- `site:medium.com "<seed-title>" "<industry>"` (writers / thought
  leaders on the same topic)

**Designer seeds** — use the platform list in
`../designer-link-discovery/references/platform-catalog.md` instead of
re-deriving it. That catalog already groups platforms by discipline
(product / UX / visual / brand / motion / design systems).

**Handle-reuse for cross-platform sourcing** — when sourcing engineers or
designers who reuse a handle across platforms, find one handle and try
it on each platform in the catalog. This is more useful for the
`$designer-link-discovery` workflow than for similarity search, but it
can occasionally surface a similar candidate when an open-source
contributor's handle leads to their LinkedIn.

## Confidence model

Rate every candidate with one of three levels. Always name the seed
attributes behind the rating.

### Strong match
Title (or close synonym) **and** seniority match, **and** at least two of:
- same company type or tier (startup / scale-up / enterprise / agency),
- a top-2 skill in common,
- same industry / vertical,
- same city or region.

### Possible match
Title or seniority matches, **plus** at least one supporting attribute
from the list above, **and** no signal contradicts the match (e.g. a
"senior" seed and a "junior" candidate is not a Possible match on title
alone).

### Weak match
Single-attribute overlap, or strong overlap on side signals (skills,
school) with no title / seniority alignment. Surface these in a separate
overflow group rather than mixing them into the main Candidates Found
list, or clearly label them so the user can skip them.

## Disambiguation for common names

When a candidate has a common name, assume multiple distinct people exist
until the signals separate them.
- Anchor every match to a distinctive detail: a specific employer, an
  unusual city, a niche skill, or the LinkedIn vanity-URL slug.
- Compare profile photos across platforms — a reused photo is a strong
  tie.
- If two profiles appearing to be the same person conflict (different
  cities, different employers), they are probably two people — do not
  merge them.
- If the seed candidate themselves appears in the search results, drop
  them; the skill is for finding *other* people.
- Never present a guessed candidate as a real match. Downgrade to Weak
  or drop entirely, and explain the ambiguity.

## Ethics & privacy

- Stay within professional, public information: titles, employers,
  skills, portfolios, professional social accounts, public writing.
- Do not search for or report private personal information: home address,
  personal phone, personal email, family members, dating profiles, or
  anything unrelated to professional work. If such a result appears, drop
  it.
- Report what is publicly visible; do not attempt to bypass logins,
  paywalls, or privacy settings.
- The goal is to widen the top of a fair hiring funnel — not to build
  dossiers on individuals.
