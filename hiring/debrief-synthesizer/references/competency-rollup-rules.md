# Competency Roll-up Rules

How to aggregate per-round 1-4 competency ratings into a defensible roll-up that does not erase signal. The cardinal rule: **show the range, not just the average.**

## Inputs

Per-round scorecards from `$portfolio-reviewer`, `$case-study-evaluation`, and `$evaluate-hiring-manager-screen`. Each scorecard rates a subset of the 6 competencies defined in `../../references/design-competencies.md` on a 1-4 scale, with cited evidence.

Round/competency coverage (typical, but vary by loop):

| Round | Competencies Typically Assessed |
|-------|----------------------------------|
| Portfolio review | All 6 (one rating per competency per case study, then per-candidate roll-up) |
| Case study — take-home | Product, Research, Craft, Ownership (primary); Systems, AI Fluency (secondary) |
| Case study — live whiteboard | Product, Research, Ownership (primary); Systems (secondary) |
| Case study — live Figma | Craft, Systems, Research (primary); Ownership, AI Fluency (secondary) |
| HM screen | All 6 optionally; only scored where signal was observed |

## Roll-up Per Competency

For each of the 6 competencies, compute and present **all four** of the following — never just one.

1. **Rounds that touched it** (count). If 0 → mark `not assessed`.
2. **Range** as `min–max` (e.g., `2–4`).
3. **Modal rating** (most common). If tied, present both.
4. **Coverage status:**
   - `strong coverage` — 3+ rounds rated this competency.
   - `partial coverage` — 1-2 rounds rated this competency.
   - `not assessed` — no round rated this competency.

### Presentation Format

Use this table shape in the output:

| Competency | Rounds | Range | Modal | Coverage |
|------------|--------|-------|-------|----------|
| Product & Strategic Impact | 3 | 3–4 | 3 | strong |
| Craft & Experience Quality | 3 | 2–4 | 3 | strong (dissent) |
| Customer-Centric Research & Insight | 2 | 3–3 | 3 | partial |
| Systems & Platform Thinking | 1 | 2–2 | 2 | partial |
| AI Fluency & Automation Leverage | 0 | — | — | not assessed |
| Ownership, Leadership & Collaboration | 3 | 3–4 | 3 | strong |

Append `(dissent)` to the Coverage column when the range is ≥ 2 — this is the visual cue that this row is a debrief discussion item.

## Rules

### DO
- Always show the range. The 1-4 scale is too narrow for an average to be informative.
- Flag any competency where rounds rated it `not assessed` if the role requires it. Coverage gaps are a recommendation input.
- Present the modal rating, not the mean, when a single number is needed for level calibration.
- Cite at least one piece of evidence per rating in the source rounds (the scorecards already include this — preserve the references).

### DON'T
- Never compute or present a mean rating. `(3 + 4 + 2) / 3 = 3.0` makes a 2–4 dissent invisible. The job of this skill is to make dissent visible.
- Never round-trip a `lean yes` verdict into a numeric rating. Per-round verdicts are surfaced separately in the Scorecard Inventory.
- Never include unsupported ratings (no cited evidence) in the roll-up. Flag and exclude.
- Never include `$de-linkedin-profile-evaluation` output in the roll-up. It uses a different scale (`good fit / possible fit / not a fit`) and is top-of-funnel context only.

## Edge Cases

- **Portfolio review provides one rating per competency per case study.** Roll those up to one rating per competency for the portfolio round (use the modal across the candidate's case studies, surface the range as the portfolio's internal spread).
- **A round assesses a competency as "Not assessed" explicitly** (HM screen pattern): treat as not contributing to the roll-up, but reduce the coverage count.
- **Two ratings on the same round** (e.g., two HM screens): treat each as its own round in the roll-up for spread purposes.
- **Competency required by role but `not assessed` at end-of-loop:** flag in `Risks & Open Questions` and lower the recommendation confidence.

## Coverage Status → Confidence Influence

The roll-up feeds the recommendation confidence (see `recommendation-rubric.md`):

| Competency Coverage | Confidence Impact |
|---------------------|-------------------|
| All 6 competencies at `strong` coverage | High confidence available |
| Any required competency at `partial` coverage | Cap confidence at medium |
| Any required competency `not assessed` | Cap confidence at low; in mid-loop, this is typically a `probe-gap` trigger |
| Any competency in `dissent` (range ≥ 2) | Confidence drops one level until dissent is addressed in the debrief |
