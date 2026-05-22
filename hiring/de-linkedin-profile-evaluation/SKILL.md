---
name: de-linkedin-profile-evaluation
description: "Evaluate a candidate's LinkedIn profile to decide whether they are worth pursuing for a design engineer role. Use when the input is a pasted LinkedIn profile and the role is design engineer — not a portfolio, screen notes, or exercise notes. Produces a simple fit verdict backed by a signal check and a responsibilities match."
---

# LinkedIn Profile Evaluation

## Overview

Use this skill to make the first judgment call in a design engineer search: given
a candidate's LinkedIn profile, is this person worth pursuing? It checks the
profile against a short list of signals and a design engineer responsibilities
checklist, then returns a simple verdict — good fit, possible fit, or not a fit.

This skill is for hiring managers, recruiters, and sourcers screening at the top
of the funnel. It is deliberately lightweight: it is a triage step, not a hiring
decision. Every claim it makes must point to specific text in the profile.

Input is **pasted LinkedIn profile text**. LinkedIn blocks automated access, so a
bare `linkedin.com/in/` URL cannot be reliably read — ask the user to paste the
profile content (headline, about, experience, skills) if they only provide a link.

## Workflow

1. Take the profile input.
- The input is the pasted text of a candidate's LinkedIn profile.
- If the user provides only a `linkedin.com/in/` URL with no profile text, ask
  them to paste the profile content (headline, about section, experience entries,
  skills) — the profile cannot be reliably fetched from the URL alone.
- Capture the basics: name (if given), current title and company, and a rough
  sense of years in the field.

2. Run the signal check.
- Work through the four signals in `references/design-engineer-criteria.md`,
  starting with the required title gate.
- **Qualifying title (required gate):** confirm the candidate has held a title of
  design engineer, UX engineer, UI engineer, or design technologist at some point
  in their career. If they never have, the verdict is "Not a fit" — state this and
  explain why, but still complete the rest of the evaluation for context.
- **Career progression (strong bonus):** note whether they held a product design
  role earlier and moved into design engineering.
- **User-centered language (bonus):** note whether the profile mentions users or a
  user-centered approach.
- **Design portfolio:** look for a portfolio link on the profile.

3. Find the portfolio if it is missing.
- If no portfolio link appears anywhere on the profile, call
  `$designer-link-discovery` to search for one before reporting it as missing.
- Never report the portfolio as missing without running `$designer-link-discovery`.

4. Match the profile against the responsibilities.
- Work through the design engineer responsibilities checklist in
  `references/design-engineer-criteria.md`.
- For each responsibility, decide whether the profile shows evidence for it, and
  cite the specific profile text that supports the call.
- Mark responsibilities with no supporting evidence as "Not shown" rather than
  guessing.

5. Produce the verdict.
- Use `references/design-engineer-criteria.md` for the criteria definitions.
- Give a simple recommendation — good fit, possible fit, or not a fit — with one
  or two sentences of reasoning grounded in the signal check and responsibilities
  match.

## Output Contract

Always return sections in this order:
- `Candidate Snapshot`
- `Signal Check`
- `Responsibilities Match`
- `Portfolio`
- `Recommendation`

## Quality Bar

Revise before finalizing if any of these are true:
- A verdict is given without running the required qualifying-title gate.
- Any claim about the candidate is not backed by specific text from the profile.
- The portfolio is reported as missing without calling `$designer-link-discovery`.
- A responsibility is marked met or not shown without citing the profile evidence
  (or its absence).
- The recommendation is not one of the three verdicts — good fit, possible fit,
  not a fit.

## Reference Navigation

Read only what is needed:
- signals, the qualifying-title list, and the responsibilities checklist:
  `references/design-engineer-criteria.md`

## Trigger Examples

Positive:
- "Here's a LinkedIn profile — is this person a fit for our design engineer role?"
- "Screen this LinkedIn profile for a design engineer opening."
- "Should we reach out to this candidate for the design engineer role?"

Negative:
- "Review this candidate's portfolio." (use `$portfolio-reviewer` — input is a
  portfolio, not a LinkedIn profile)
- "Find this designer's portfolio and other online links." (use
  `$designer-link-discovery` — the task is link discovery, not fit evaluation)
- "Debrief this hiring manager screen." (use `$evaluate-hiring-manager-screen` —
  input is screen notes, not a profile)

Ambiguous:
- "Evaluate this candidate." (clarify: is the input a pasted LinkedIn profile, a
  portfolio, or screen notes?)
- "Here's a linkedin.com/in/ link." (ask the user to paste the profile text — the
  profile cannot be reliably read from the URL alone)
