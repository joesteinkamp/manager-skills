# Recommendation Rubric

How to turn a competency roll-up + dissent calls + level calibration into a defensible recommendation. Two modes: **end-of-loop** (verdict) and **mid-loop** (next-step).

## Confidence Levels

Every recommendation in either mode carries a confidence label.

| Confidence | When to use |
|-----------|-------------|
| **High** | All required competencies at strong coverage, modal ratings meet or exceed level expectations, no unresolved dissent flags, no consensus-breaking single-voice dissent. |
| **Medium** | At least one required competency at partial coverage, OR one unresolved dissent flag, OR the candidate is borderline against level expectations. |
| **Low** | A required competency is not assessed, OR multiple unresolved dissent flags, OR per-round verdicts span 3+ steps (`strong yes` and `strong no` in the same loop). |

A loop can produce a `strong yes` at low confidence — the recommendation reflects the signal, the confidence reflects how solid the signal is. Always present both.

## End-of-Loop Mode

Produce one of: `strong yes`, `lean yes`, `lean no`, `strong no`.

### Decision Inputs

- The modal rating per competency, compared against level expectations from `../../references/design-competencies.md`.
- The per-round verdicts (already produced by `$portfolio-reviewer`, `$case-study-evaluation`, etc.).
- Open dissent flags.
- Coverage status across the 6 competencies.

### Verdict Definitions

- **Strong yes:** Modal ratings meet or exceed level expectations on every required competency. Per-round verdicts are majority `strong yes / lean yes` with no `strong no`. No unresolved high-severity dissent.
- **Lean yes:** Modal ratings meet expectations on most required competencies, with at most one at the borderline of below. Per-round verdicts skew yes. Dissent flags exist but the consensus side is supported.
- **Lean no:** Modal ratings below expectations on a required competency, OR per-round verdicts skew no, OR a single-low-voice flag points to a real concern that the debrief should address.
- **Strong no:** Multiple modal ratings below level expectations, OR per-round verdicts include `strong no` with supporting evidence the rest of the loop did not refute.

### Required Output

Each recommendation must include:
- Verdict + confidence on the same line.
- The 2-3 competencies and rounds driving the verdict (cited).
- Any unresolved dissent flagged for debrief discussion.
- The decision the debrief needs to make: ratify, escalate to another round, or decline.

## Mid-Loop Mode

Produce one of: `continue`, `kill`, `probe-gap`. **Never produce a hire/no-hire verdict in mid-loop mode.**

### Decision Tree

1. **Is there a required competency rated below expectations with strong coverage so far?**
   - Yes → `kill` (further rounds unlikely to change the verdict).
2. **Is there a required competency `not assessed`, with the rest of the signal positive?**
   - Yes → `probe-gap` (name the competency and the round type that would close it).
3. **Is there an unresolved dissent flag on a competency the candidate would be hired for?**
   - Yes → `probe-gap` targeting that competency (a different round type often resolves dissent).
4. **Are modal ratings at or above expectations on all assessed competencies, with full coverage to come?**
   - Yes → `continue`.
5. **Otherwise** → `continue` and note what the remaining rounds need to surface.

### Round Type → Competency Coverage (for `probe-gap`)

When recommending a round to close a gap, choose the round type that most reliably surfaces the missing competency:

| Competency to probe | Best round type |
|---------------------|-----------------|
| Product & Strategic Impact | Take-home or live whiteboard case study |
| Craft & Experience Quality | Live Figma case study; portfolio deep-dive |
| Customer-Centric Research & Insight | Take-home case study; HM screen on a past project |
| Systems & Platform Thinking | Live Figma case study; design system architecture interview |
| AI Fluency & Automation Leverage | Take-home with AI tools allowed; HM screen on workflow |
| Ownership, Leadership & Collaboration | HM screen; cross-functional partner interview (PM/eng) |

### Required Output

Each mid-loop recommendation must include:
- The decision (`continue` / `kill` / `probe-gap`) + confidence.
- If `probe-gap`: the specific competency, the recommended round type, and the question the round needs to answer.
- If `kill`: the specific competency and evidence driving the decision; do not present subjective summary.
- If `continue`: what the remaining planned rounds need to surface for the loop to reach a confident verdict.

## Anti-Patterns

- ❌ A `strong yes` recommendation that does not name confidence.
- ❌ A `probe-gap` recommendation that says "do another round" without naming the round type or the competency.
- ❌ A mid-loop synthesis that says `hire` or `no hire`. The mode is `continue / kill / probe-gap` — discipline matters.
- ❌ A verdict that does not cite specific rounds and competencies. Defensibility requires sources.
- ❌ A high-confidence verdict when a required competency is `not assessed`. Coverage gaps cap confidence.
