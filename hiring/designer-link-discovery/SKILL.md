---
name: designer-link-discovery
description: "Discover and verify the professional online links connected to a designer's LinkedIn profile — portfolio site, Dribbble, Behance, Medium, X, GitHub, and more — and return an annotated, confidence-rated link inventory. Use when the starting point is a LinkedIn profile or a designer's name and you need to assemble their full body of work for hiring research, not evaluate work you already have."
---

# Designer Link Discovery

## Overview

Use this skill to find every relevant professional online link connected to a
design candidate, starting from their LinkedIn profile. It harvests links the
profile already exposes, searches the platforms designers actually use, follows
the link graph outward, verifies that each link belongs to the same person, and
returns an annotated inventory where every link carries a confidence rating and
a one-line note.

This is the step *before* portfolio evaluation. Hiring managers, recruiters, and
sourcers often start with only a LinkedIn profile and have to manually hunt down
the candidate's actual work — portfolio, Dribbble, Behance, Medium, X, GitHub.
This skill does that discovery and hands a clean inventory to `$portfolio-reviewer`
or to a candidate record.

This skill is model-agnostic and is designed to run in a browser context (for
example, as a Chrome skill). When it runs in the browser it reads the LinkedIn
profile in the active tab; when the profile is unavailable or login-gated it
falls back to details the user pastes in. It uses whatever web search and
page-reading capabilities the host environment provides — do not assume a
specific tool name.

**Privacy boundary — this is not optional.** Surface only professional, public
links: portfolios, design communities, writing, code, and professional social
accounts. Never surface or search for home addresses, personal phone numbers,
personal email, family members, dating profiles, or anything outside a
professional sourcing context. If a search turns up that kind of result, drop it
and do not report it.

## Workflow

1. Establish the subject.
- Read the LinkedIn profile open in the active browser tab. If no profile is
  available, or it is login-gated, ask the user to paste the designer's name,
  current role and company, location, and headline.
- Capture disambiguating signals: full name (and any prior names), current and
  past employers, city/region, and the LinkedIn vanity URL slug.
- Note the design discipline (product / UX / visual / brand / motion / design
  systems) — it changes which platforms matter. A motion designer is on Vimeo;
  a visual designer is on Dribbble and Behance; a design-systems person is on
  GitHub and Figma Community.

2. Harvest links already on LinkedIn.
- Pull links from the Contact Info section, the Featured section, the About
  text, the Activity feed, and individual experience entries.
- Treat these as Confirmed seeds — the candidate published them on their own
  profile.

3. Run platform discovery.
- Work through the platform list in `references/platform-catalog.md`.
- For each platform, use the search-query patterns in
  `references/discovery-playbook.md` (name searches, `site:` searches,
  handle-reuse searches).
- Prioritize platforms that match the candidate's discipline; do not skip the
  staples (portfolio site, Dribbble, Behance, Medium, X, GitHub).

4. Follow the link graph.
- Each profile you find usually links onward — a Dribbble bio links to the
  portfolio, a portfolio footer links to X and GitHub, a Medium bio links back
  to LinkedIn. Crawl outward until no new links appear.
- A handle reused across platforms (`@janedesigns` on X, Dribbble, and GitHub)
  is a strong same-person signal — chase reused handles deliberately.

5. Verify identity and disambiguate.
- For every candidate link, apply the matching signals in
  `references/discovery-playbook.md`: explicit cross-link, reused handle,
  matching profile photo, matching employer / location / discipline.
- For common names, assume multiple people until the signals separate them.
  Never merge two people into one inventory.

6. Assign confidence and annotate.
- Rate each link **Confirmed**, **Probable**, or **Unverified** using the
  confidence model in `references/discovery-playbook.md`.
- Name the signal behind a Confirmed or Probable rating ("listed in LinkedIn
  Contact Info"; "portfolio footer links to this X account").
- Write a one-line note for each link: what it is, how active it is, and why it
  matters for a hiring review.

7. Assemble the inventory.
- Use `references/link-inventory-template.md` for the response structure.
- List the platforms you checked and found nothing on, so the reader can see
  coverage rather than guessing what was missed.

## Output Contract

Always return sections in this order:
- `Discovery Context`
- `Link Inventory` (grouped by category; every link annotated with confidence)
- `Needs Verification`
- `Coverage Summary`
- `Recommended Next Steps`

## Quality Bar

Revise before finalizing if any of these are true:
- Any link is listed without a confidence rating (Confirmed / Probable /
  Unverified).
- A link is rated Confirmed or Probable without naming the signal that supports
  it ("Confirmed" with no reason given).
- The candidate has a common name and no disambiguation was done — links are
  presented as theirs with no statement of how they were tied to this person.
- Speculative or low-confidence links are mixed into the main inventory instead
  of being isolated in `Needs Verification`.
- The LinkedIn profile's own Contact Info and Featured links were not harvested.
- There is no coverage information — the reader cannot tell which platforms were
  actually checked.
- Any non-professional or private personal information was surfaced (home
  address, personal phone, family, etc.) — this must be removed entirely.
- A link's note is generic ("their portfolio") instead of useful ("portfolio,
  6 case studies, last updated 2025 — strong fintech work").

## Reference Navigation

Read only what is needed:
- platforms to check, URL patterns, and where each link tends to surface:
  `references/platform-catalog.md`
- search-query patterns and the confidence / disambiguation model:
  `references/discovery-playbook.md`
- output structure and a worked example: `references/link-inventory-template.md`

The shared `../references/design-competencies.md` is for the evaluation skills
and is not needed here — this skill discovers links, it does not score work.

## Trigger Examples

Positive:
- "Find all the links connected to this designer's LinkedIn profile."
- "I'm looking at a candidate on LinkedIn — find their portfolio, Dribbble, and writing."
- "Pull together every online profile for this designer so I can review their work."
- "Where else does this candidate publish — Medium, X, GitHub?"

Negative:
- "Review this candidate's portfolio." (use `$portfolio-reviewer` — input is a
  portfolio, and the task is evaluation, not discovery)
- "Evaluate this candidate's case study exercise." (use `$case-study-evaluation`)
- "Debrief this hiring manager screen." (use `$evaluate-hiring-manager-screen`)

Ambiguous:
- "Research this candidate." (clarify: discover their online links, or evaluate
  work you already have?)
- "Find this person online." (confirm this is professional hiring research and
  scope the search to public, professional links only)
- "Get me this designer's contact details." (clarify: professional profiles and
  portfolio only — this skill does not surface private contact information)
