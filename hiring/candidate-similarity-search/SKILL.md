---
name: candidate-similarity-search
description: "Find more candidates like a strong seed LinkedIn profile. Extracts the seed's keywords and attributes (title, seniority, companies, skills, industry, education, location), generates a search playbook (Google `site:linkedin.com/in/` queries, prebuilt LinkedIn search URLs, and general web/portfolio searches), executes the searches available in the environment, and returns ranked candidate matches with the matching attributes called out. Use when the input is a LinkedIn profile and the task is to source similar people — not to evaluate one profile for fit (use `$de-linkedin-profile-evaluation`) and not to find one person's other online profiles (use `$designer-link-discovery`)."
---

# Candidate Similarity Search

## Overview

Use this skill to turn one strong candidate into a pipeline of similar ones.
Given a seed LinkedIn profile, it pulls out the keywords and attributes that
make the seed interesting — role, seniority, company tier, skills, industry,
education, location — and uses those attributes to search for other people
who match. It returns an attribute breakdown, a copy-pasteable search
playbook, and any candidates it surfaced while running the searches.

This skill is for recruiters and sourcers expanding the top of the funnel.
It is role-agnostic: the seed can be a designer, engineer, PM, marketer, or
anything else on LinkedIn. It is also intentionally a sourcing tool, not a
fit verdict — every candidate it surfaces should still be screened with
`$de-linkedin-profile-evaluation` (or a role-specific equivalent) before
outreach.

This skill is model-agnostic and is designed to run in either a browser
context (reading the LinkedIn profile in the active tab) or a CLI / chat
context (using profile text the user pastes). It uses whatever web search
and page-reading capabilities the host environment provides — do not assume
a specific tool name. When the environment cannot execute a search, the
skill still produces the playbook so the user can run it themselves.

**Privacy boundary — this is not optional.** Surface only professional,
public information: titles, employers, skills, professional profiles,
portfolios, public writing. Never search for or report home addresses,
personal phone numbers, personal email, family members, dating profiles, or
anything outside a professional sourcing context. If a search turns up that
kind of result, drop it and do not report it.

## Workflow

1. Establish the seed profile.
- If a LinkedIn profile is open in the active browser tab, read it there.
- Otherwise ask the user to paste the seed's headline, About section,
  Experience entries, Skills, and Education. A bare `linkedin.com/in/` URL
  cannot be reliably fetched and is not enough on its own.
- Capture name, current title and company, location, and the LinkedIn
  vanity slug for later disambiguation.

2. Extract attributes.
- Work through the taxonomy in `references/attribute-extraction.md` and
  pull every category that the profile actually shows.
- For each extracted attribute, cite the profile text it came from.
- Mark categories the profile does not show as "not stated" — never guess.

3. Confirm the similarity axis.
- Some attributes will matter more than others depending on what the user
  is sourcing for. If the request is ambiguous, ask the user which
  attributes are "must match" vs "nice to match" (for example: "same title
  at any company", "same skills regardless of title", "same industry,
  similar seniority").
- If the user does not specify, default to: **current title + seniority +
  the two strongest skills + industry**, and state that default in the
  output so the user can correct it.

4. Generate the search playbook.
- Use `references/search-playbook.md` to build three groups of queries:
  Google `site:linkedin.com/in/` queries, prebuilt LinkedIn search URLs,
  and general web / portfolio queries.
- Label every query with which seed attributes it targets, so the user
  can re-run the ones that match their priorities.
- When the seed is a designer, point to
  `../designer-link-discovery/references/platform-catalog.md` for the
  general-web platform list rather than redefining it here.

5. Execute the searches the environment supports.
- Run whatever subset of the playbook the host environment allows
  (typically Google searches; LinkedIn URLs almost always require the
  user's logged-in session). State up front which queries you executed
  and which you left for the user.
- For each surfaced profile, capture: profile URL, name, current title and
  company, location, and which seed attributes it shares.

6. Disambiguate and rate every candidate.
- Apply the confidence model in `references/search-playbook.md`: **Strong
  match**, **Possible match**, or **Weak match** — and name the attributes
  behind the rating.
- For common names, follow the disambiguation rules in
  `references/search-playbook.md`. Never present a guessed match as the
  same person; downgrade or drop it.
- Drop anyone who appears to be the seed candidate themselves.

7. Assemble the output.
- Use `references/candidate-list-template.md` for the response structure.
- List which sources you searched and which you left for the user, so the
  reader can see coverage rather than guessing what was missed.

## Output Contract

Always return sections in this order:
- `Seed Snapshot`
- `Attribute Profile` (grouped by category; signal strength noted)
- `Search Playbook` (grouped by source: Google `site:`, LinkedIn URLs, general web)
- `Candidates Found` (ranked; every entry annotated with confidence and matching attributes)
- `Coverage Summary`
- `Recommended Next Steps`

## Quality Bar

Revise before finalizing if any of these are true:
- A candidate is listed without a confidence rating (Strong / Possible /
  Weak) or without naming which seed attributes matched.
- Any attribute in the Attribute Profile is not backed by specific text
  from the seed profile.
- The Search Playbook contains queries that are not copy-pasteable, or
  queries with no label saying which attributes they target.
- A common-name candidate is presented as a match with no disambiguation.
- The seed candidate themselves appears in `Candidates Found`.
- Coverage Summary is missing — the reader cannot tell which queries were
  actually executed vs left for the user.
- The skill produced a fit verdict ("good fit / not a fit"). Fit
  evaluation is `$de-linkedin-profile-evaluation`'s job, not this skill's.
- Any non-professional or private personal information was surfaced (home
  address, personal phone, family, etc.) — this must be removed entirely.

## Reference Navigation

Read only what is needed:
- attribute taxonomy, weighting rubric, and evidence rule:
  `references/attribute-extraction.md`
- query patterns for the three sources, confidence model, and
  disambiguation rules: `references/search-playbook.md`
- output structure and a worked example: `references/candidate-list-template.md`

When the seed is a designer, also read
`../designer-link-discovery/references/platform-catalog.md` for the
general-web platform list — do not re-derive it.

## Trigger Examples

Positive:
- "Find more candidates like this LinkedIn profile."
- "Source me people similar to this designer / engineer / PM."
- "This person is great — who else looks like them?"
- "Run a similarity search off this profile and give me a sourcing list."

Negative:
- "Is this person a fit for our design engineer role?" (use
  `$de-linkedin-profile-evaluation` — the task is fit evaluation of one
  profile, not similarity search.)
- "Find this designer's portfolio and other online links." (use
  `$designer-link-discovery` — the task is one person's link inventory,
  not finding similar people.)
- "Review this candidate's portfolio." (use `$portfolio-reviewer`.)

Ambiguous:
- "Find me more like this." (confirm the seed is a LinkedIn profile and
  ask which attributes matter most — title, company tier, skills,
  industry, location.)
- "Source for this role." (clarify: do they have a seed candidate to
  search from, or only a role description? This skill needs a seed.)
- "Here's a `linkedin.com/in/` link." (ask the user to paste the profile
  text — the profile cannot be reliably read from the URL alone.)
