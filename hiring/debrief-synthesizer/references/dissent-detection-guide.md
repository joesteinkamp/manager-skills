# Dissent Detection Guide

How to detect, name, and frame disagreement in a hiring loop. The job of this skill is to **surface dissent, not flatten it.** Averaging conflicting ratings into a single number is the most common debrief failure mode and the one this guide is designed to prevent.

## What Counts as Dissent

Four detection rules. Apply all four to every loop.

### 1. Spread Dissent (rating-level)

A single competency receives ratings with a range ≥ 2 across rounds.

| Example | Dissent? |
|---------|----------|
| Craft rated 3, 4, 3 across three rounds | No (range 1) |
| Craft rated 2, 4, 3 across three rounds | **Yes** (range 2) |
| Systems rated 1, 4 across two rounds | **Yes** (range 3) — strong dissent |

### 2. Verdict Dissent (round-level)

Any interviewer's per-round hiring recommendation differs from the majority by 2+ levels on the 4-step scale `strong yes / lean yes / lean no / strong no`.

| Example | Dissent? |
|---------|----------|
| Two rounds `lean yes`, one round `strong yes` | No (one step) |
| Two rounds `lean yes`, one round `lean no` | **Yes** (two steps — the line that matters) |
| Mixed `strong yes` and `strong no` | **Yes** (three steps — escalate to a re-debrief) |

### 3. Single-Low-Voice

One interviewer rates 1 or 2 on a competency while all others rate 3 or 4. Even if the spread rule doesn't trip, this asymmetry deserves attention because it often indicates either a real concern the rest of the loop missed *or* an interviewer-specific bias.

### 4. Single-High-Voice

The mirror: one interviewer rates 4 while all others rate 2 or 3. Often indicates either a unique strength one interviewer saw *or* a halo effect. Worth a debrief question either way.

## How to Frame Dissent

### DO
- **Name the interviewers on each side.** "Alex (HM screen) scored Craft 2 against Sarah (portfolio) and Priya (case study) at 3" — not "There was some disagreement on Craft."
- **Quote the conflicting evidence verbatim** from each scorecard. The debrief needs the actual words, not summaries.
- **State the round type next to each name.** The same competency surfaces differently in a portfolio than in a live whiteboard. Round type contextualizes the rating.
- **Lead with the most disputed competency** in the dissent section. Don't bury it after the consensus areas.
- **Pose the open question** the debrief needs to resolve: "Is Alex seeing something the others missed, or is the portfolio overstating craft because the case studies are static rather than live?"

### DON'T
- Never paraphrase dissent into "mixed signals." That is the failure mode this skill exists to prevent.
- Never average dissenting ratings to a single number.
- Never drop a lone dissenting voice on the basis of majority alone — investigate it explicitly.
- Never frame dissent as a problem with the interviewer ("Alex was harsh"). The dissent is information.

## Dissent Framing Template

For each detected dissent flag, write a paragraph using this shape:

> **[Competency or verdict]** — [round-type interviewer] rated [N], [round-type interviewer] rated [N], [round-type interviewer] rated [N]. The low-side cited [quote from low-side scorecard]; the high-side cited [quote from high-side scorecard]. **Open question for debrief:** [the specific question the loop needs to resolve, framed neutrally].

### Example

> **Craft & Experience Quality** — Sarah (portfolio) rated 3, Priya (case study, live Figma) rated 4, Alex (HM screen) rated 2. The high-side cited "candidate built a working multi-state flow in 45 minutes with attention to error states and tap targets"; the low-side cited "explanation of design system trade-offs was confused; could not articulate when to make a one-off vs. extend the system." **Open question for debrief:** Is craft strong in execution but weak in articulating system-level decisions — and if so, does that matter at the Practitioner (P) level we're hiring for?

## Confidence Effects

Each unresolved dissent flag lowers the recommendation confidence one level. The debrief is the resolution mechanism — if the loop discusses dissent and converges, confidence can be restored. The synthesizer surfaces; the humans resolve.

## Anti-Patterns to Catch and Fix

- ❌ "There were some differing opinions on craft." → Name the interviewers, state the ratings, quote evidence.
- ❌ "The loop averaged to a 3 on Systems thinking." → Show the range. If it was 1 and 4, that's not a 3, that's a flag.
- ❌ "Majority of the loop said yes." → If one voice said `strong no`, that voice needs a paragraph.
- ❌ "The HM screen scored lower across the board." → Why? Round-type or interviewer-specific? Make the loop discuss it.
