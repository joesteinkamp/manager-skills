---
name: debrief-synthesizer
description: "Synthesize scorecards from a design hiring loop into a hire/no-hire recommendation with dissent surfaced. Takes the outputs of `$portfolio-reviewer`, `$case-study-evaluation`, and `$evaluate-hiring-manager-screen`, rolls up the 1-4 competency ratings across rounds, detects rating spread > 1 as dissent, calibrates to the target Career Mapper level (E/P/I/A/S), and produces a defensible verdict. Supports end-of-loop synthesis (full hire/no-hire) and mid-loop synthesis (continue / kill / probe-specific-gap with the round needed to close the gap). Use after multiple interviewers have completed scorecards — not for a single round (use the per-round skill directly)."
---

# Debrief Synthesizer

## Overview

Use this skill to synthesize per-round scorecards from a design hiring loop into a defensible recommendation. Accepts scorecards from any combination of `$portfolio-reviewer`, `$case-study-evaluation`, and `$evaluate-hiring-manager-screen`, plus the role, target level, and loop structure. Produces a competency roll-up across rounds, explicit dissent calls, level calibration, and a recommendation calibrated to the loop state.

Two modes:
- **End-of-loop:** the full loop is complete (typically portfolio + case study + HM screen, plus any additional rounds). Produces a `strong yes / lean yes / lean no / strong no` verdict.
- **Mid-loop:** at least one but not all scorecards are present. Produces a `continue / kill / probe-gap` recommendation, naming the specific competency gap and the round type that would close it.

The job of this skill is to prevent two failure modes in hiring debriefs: (1) **groupthink** that smooths over a strong dissenting interviewer, and (2) **the loudest voice in the debrief winning** — by surfacing rating spread, naming dissenting interviewers, and forcing the recommendation to confront disagreement instead of averaging it away.

Output is formatted for use in Greenhouse, Lever, Ashby, or as a debrief doc in Notion or Google Docs. When the target ATS is specified, adapt the scorecard summary format accordingly.

## Workflow

1. Establish loop context.
- Identify the role, target level on the Career Mapper (E / P / I / A / S), and team context.
- Catalog which scorecards are provided. Detect the mode:
  - All expected rounds present → **end-of-loop**.
  - At least one but not all → **mid-loop** (note which rounds are missing).
- Identify each interviewer by name + round type (so dissent can be attributed).
- If a `$de-linkedin-profile-evaluation` verdict is provided, capture it as top-of-funnel context only — it does not feed the competency roll-up.

2. Normalize the scorecards.
- For each scorecard, extract per-competency ratings on the shared 1-4 scale defined in `../references/design-competencies.md`.
- Pull the cited evidence for each rating. Drop any rating that lacks evidence — flag as "unsupported" and exclude from the roll-up.
- Record the per-round hiring recommendation if present (`strong yes / lean yes / lean no / strong no`).
- Track competency coverage: which of the 6 competencies were assessed in any round, with how much signal.

3. Roll up the competencies.
- For each of the 6 competencies, compute:
  - **Rounds that touched it** (count).
  - **Range** (min and max rating across rounds).
  - **Modal rating** (most common across rounds).
  - **Coverage status:** `strong coverage` (3+ rounds), `partial coverage` (1-2 rounds), `not assessed`.
- Per the rules in `references/competency-rollup-rules.md`, never present a single averaged number — always show the range plus the source rounds.

4. Detect dissent.
- Apply the rules in `references/dissent-detection-guide.md`:
  - **Spread dissent:** rating range ≥ 2 points on a single competency → flag.
  - **Verdict dissent:** any interviewer's hiring recommendation differs from the majority by 2+ levels (e.g., `strong yes` vs. `lean no`) → flag.
  - **Single-low-voice:** one interviewer at 1-2 while all others are at 3-4 → flag and name the interviewer.
  - **Single-high-voice:** one interviewer at 4 while all others are at 2-3 → flag and name the interviewer.
- For every flag, name the interviewers on each side and quote the conflicting evidence. Do not average away.

5. Calibrate to the target level.
- Read level expectations from `../references/design-competencies.md` (E / P / I / A / S).
- For each competency, compare the modal rating against the level's expected demonstration:
  - Below expectations for the target level → flag as a gap.
  - At expectations → confirm.
  - Above expectations → note (do not over-weight).
- Flag any competency that is consistently below the target level across multiple rounds.

6. Generate the recommendation.
- Apply the verdict rubric in `references/recommendation-rubric.md`:
  - **End-of-loop mode:** produce `strong yes / lean yes / lean no / strong no` with a confidence level (`high / medium / low`). Confidence drops when dissent is unresolved or coverage is thin on key competencies.
  - **Mid-loop mode:** produce `continue / kill / probe-gap`. If `probe-gap`, name the specific competency gap and the round type that would close it (e.g., "probe Systems & Platform Thinking with a Live Figma exercise"). Never produce a hire/no-hire verdict in mid-loop mode.
- Every recommendation must cite the rounds and competencies driving it.

7. Build a debrief meeting agenda.
- Open with a 1-minute candidate snapshot.
- Lead with the dissent: discuss the most disputed competency first, before consensus areas.
- Include one explicit "challenge our consensus" prompt — counter-bias against groupthink.
- Close with a recommendation read-out and an explicit ask: does the loop agree?
- For mid-loop, the agenda focuses on "continue or kill" + "what would the next round need to probe."

8. Format output.
- Use `references/debrief-template.md` for the response structure. The template has two variants — end-of-loop and mid-loop — matching the two output contracts below.

## Output Contract

The two modes have different contracts. Use the contract that matches the loop state.

**End-of-loop mode** — return sections in this order:
- `Loop Context`
- `Scorecard Inventory`
- `Competency Roll-up`
- `Dissenting Views`
- `Level Calibration`
- `Risks & Open Questions`
- `Hiring Recommendation`
- `Debrief Meeting Agenda`

**Mid-loop mode** — return sections in this order:
- `Loop Context` (with `Rounds Missing` called out)
- `Scorecard Inventory`
- `Competency Roll-up` (with `Coverage Status` per competency)
- `Dissenting Views`
- `Recommendation` (`continue / kill / probe-gap`)
- `Suggested Next Round` (if `probe-gap`)
- `Debrief Meeting Agenda`

## Quality Bar

Revise before finalizing if any of these are true:
- Any competency rating in the roll-up is presented as a single averaged number without showing the range and source rounds.
- Dissent (rating spread ≥ 2 on a competency, or verdict differing by 2+ levels) is not explicitly called out — it is averaged or paraphrased away.
- Dissenting interviewers are not named with their round type. "There was some disagreement" is not a dissent call; "Alex (HM screen) scored Craft 2 against Sarah (portfolio) and Priya (case study) at 3" is.
- Recommendation lacks a confidence level (`high / medium / low`) or does not cite the rounds and competencies driving it.
- Level calibration is missing — the synthesis does not state whether the modal ratings match the target Career Mapper level (E / P / I / A / S).
- Any competency rating is included in the roll-up without cited evidence from the source scorecard — unsupported ratings must be flagged and excluded.
- Mid-loop mode produces a hire/no-hire verdict instead of `continue / kill / probe-gap`. Never produce a final verdict on a partial loop.
- `Probe-gap` recommendations do not name the specific competency gap and the round type that would close it.
- Debrief meeting agenda omits a "challenge our consensus" prompt — this is the single biggest counter-bias against groupthink and must always be present.
- A `$de-linkedin-profile-evaluation` verdict is folded into the competency roll-up. It is top-of-funnel context only and uses a different scale (`good fit / possible fit / not a fit`) that does not normalize to 1-4.
- Recommendation is presented as if there is no uncertainty when coverage is partial or dissent is unresolved — confidence must reflect reality.

## Reference Navigation

Read only what is needed:
- shared competency definitions, level expectations, and scoring scale: `../references/design-competencies.md`
- competency roll-up math and presentation rules: `references/competency-rollup-rules.md`
- dissent detection rules and framing: `references/dissent-detection-guide.md`
- verdict rubric and mid-loop decision tree: `references/recommendation-rubric.md`
- debrief output shell (both modes): `references/debrief-template.md`

## Trigger Examples

Positive:
- "Synthesize the loop for [candidate] — I have the portfolio review, the case study scorecard, and two HM screens."
- "Run a debrief synthesis. We're undecided after three rounds."
- "We're mid-loop on [candidate] — portfolio + HM screen done, case study not scheduled yet. What should we do?"
- "Prep a debrief doc for the loop on [candidate]."
- "Roll up these scorecards and tell me where the loop disagrees."

Negative:
- "Review this candidate's portfolio." (use `$portfolio-reviewer` — single-round evaluation)
- "Evaluate this case study exercise." (use `$case-study-evaluation`)
- "Debrief this hiring manager screen." (use `$evaluate-hiring-manager-screen`)
- "Should I screen this LinkedIn profile?" (use `$de-linkedin-profile-evaluation` — top-of-funnel gate, pre-loop)
- "Find more candidates like this one." (use `$candidate-similarity-search`)

Ambiguous:
- "Is this candidate a hire?" (clarify: which rounds have been completed? Share the scorecards.)
- "Help me prep for the debrief." (clarify: which candidate, and which scorecards do you have?)
- "We disagree about [candidate] — what should we do?" (clarify: share the per-round scorecards so the disagreement can be surfaced by competency.)
