# Debrief Output Template

Output shell for `debrief-synthesizer`. Two variants — pick by mode.

---

## End-of-Loop Mode

### Loop Context

- **Candidate:**
- **Role:**
- **Target level:** (E / P / I / A / S)
- **Team / business context:**
- **Loop completed:** (yes — all rounds present)
- **Rounds included:** (e.g., portfolio review, take-home case study, HM screen #1, HM screen #2)

### Scorecard Inventory

| Round | Interviewer | Date | Per-round verdict |
|-------|-------------|------|-------------------|
| Portfolio review | | | (strong yes / lean yes / lean no / strong no) |
| Case study (format) | | | |
| HM screen | | | |
| (additional round) | | | |

### Competency Roll-up

Per `competency-rollup-rules.md`, always show range and modal — never an average.

| Competency | Rounds | Range | Modal | Coverage |
|------------|--------|-------|-------|----------|
| Product & Strategic Impact | | | | |
| Craft & Experience Quality | | | | |
| Customer-Centric Research & Insight | | | | |
| Systems & Platform Thinking | | | | |
| AI Fluency & Automation Leverage | | | | |
| Ownership, Leadership & Collaboration | | | | |

### Dissenting Views

One paragraph per flag using the template in `dissent-detection-guide.md`.

- **[Competency]:** [name] (round type) rated [N]; [name] (round type) rated [N]. Low-side cited "[quote]"; high-side cited "[quote]". **Open question for debrief:** [neutrally framed].
- **[Verdict-level dissent]:** ...

### Level Calibration

For each competency, compare modal to target level expectations.

- **[Competency]:** Modal [N] vs. [level] expectation of [N]. (Meets / below / above.) Notes:
- ...

### Risks & Open Questions

- [Specific risk tied to evidence — e.g., "AI Fluency not assessed in any round; required for the role."]
- [Open question the debrief should resolve.]

### Hiring Recommendation

**Recommendation:** [strong yes / lean yes / lean no / strong no] — **Confidence:** [high / medium / low]

**Driving competencies and rounds:**
- [Competency] — [evidence summary tied to rounds]
- [Competency] — [evidence]

**The debrief needs to decide:** [ratify / escalate to another round / decline]

### Debrief Meeting Agenda

| Block | Duration | Focus |
|-------|----------|-------|
| Candidate snapshot | 1 min | Role, level, who we have |
| Dissent first | 10 min | Walk through the disputed competencies before consensus |
| Consensus areas | 5 min | Confirm — and challenge our own consensus (anti-groupthink prompt) |
| Risks & gaps | 5 min | Coverage gaps, unanswered questions |
| Recommendation read-out | 3 min | Verdict + confidence |
| Decision | 5 min | Ratify, escalate, or decline |

**Anti-groupthink prompt (always include):**
> "Before we ratify: who would push back if they had to argue the other side of this decision? What's the strongest case against our current direction?"

---

## Mid-Loop Mode

### Loop Context

- **Candidate:**
- **Role:**
- **Target level:** (E / P / I / A / S)
- **Loop status:** mid-loop
- **Rounds completed:**
- **Rounds missing:** (call these out explicitly)

### Scorecard Inventory

Same table shape as end-of-loop, listing only completed rounds.

### Competency Roll-up

Same table shape, with `Coverage Status` per competency made prominent — coverage gaps are the central decision input in mid-loop mode.

### Dissenting Views

Same framing as end-of-loop. Even one dissent flag mid-loop is a candidate for `probe-gap`.

### Recommendation

**Decision:** [continue / kill / probe-gap] — **Confidence:** [high / medium / low]

If `continue`: what the remaining rounds need to surface.
If `kill`: the specific competency and evidence.
If `probe-gap`: see next section.

### Suggested Next Round

*(Only if `probe-gap`.)*

- **Competency to probe:** [specific competency]
- **Recommended round type:** [from `recommendation-rubric.md` mapping]
- **Question the round must answer:** [neutrally framed]
- **Interviewer suggestion:** [if applicable — different round type often means a different interviewer profile]

### Debrief Meeting Agenda

| Block | Duration | Focus |
|-------|----------|-------|
| Snapshot | 1 min | Candidate, target level, rounds completed |
| Signal so far | 10 min | Competency roll-up + dissent |
| Gap analysis | 5 min | What we know vs. what we still need |
| Decision | 5 min | Continue / kill / probe |
| Next steps | 4 min | If probe: round type, interviewer, timing |

**Anti-groupthink prompt:**
> "If we kill this candidate today, what would we regret missing? If we continue, what's the strongest reason we'd waste the next round?"

---

## Starter Example (End-of-Loop)

### Loop Context

- **Candidate:** Casey Rivera
- **Role:** Product Designer (Practitioner level)
- **Target level:** P
- **Team / business context:** B2B SaaS; growth surface; team of 4 designers
- **Loop completed:** Yes
- **Rounds included:** Portfolio review (Sarah), Take-home case study (Priya), HM screen (Alex), HM screen (Jordan)

### Scorecard Inventory

| Round | Interviewer | Date | Per-round verdict |
|-------|-------------|------|-------------------|
| Portfolio review | Sarah | May 12 | lean yes |
| Take-home case study | Priya | May 16 | strong yes |
| HM screen #1 | Alex | May 18 | lean no |
| HM screen #2 | Jordan | May 20 | lean yes |

### Competency Roll-up

| Competency | Rounds | Range | Modal | Coverage |
|------------|--------|-------|-------|----------|
| Product & Strategic Impact | 4 | 3–4 | 3 | strong |
| Craft & Experience Quality | 3 | 2–4 | 3 | strong (dissent) |
| Customer-Centric Research & Insight | 2 | 3–4 | 3 | partial |
| Systems & Platform Thinking | 2 | 2–3 | 2 | partial |
| AI Fluency & Automation Leverage | 1 | 3–3 | 3 | partial |
| Ownership, Leadership & Collaboration | 4 | 3–4 | 3 | strong |

### Dissenting Views

- **Craft & Experience Quality** — Sarah (portfolio) rated 3, Priya (take-home) rated 4, Alex (HM screen) rated 2. High-side cited "multi-state flow with thoughtful error handling, design system tokens used consistently"; low-side cited "could not articulate when to extend the design system vs. ship a one-off; treated trade-offs as taste rather than principle." **Open question for debrief:** Is craft strong in execution but weak in articulating system-level decisions — and does that matter at the P level?
- **Verdict spread** — Alex (HM screen) was `lean no`; Priya (take-home) was `strong yes`. Two-step spread. The decisive question is whether Alex's concern (systems articulation) is corroborated elsewhere or HM-screen-specific.

### Level Calibration

- **Product & Strategic Impact:** Modal 3 vs. P expectation of 3. Meets.
- **Craft:** Modal 3 vs. P expectation of 3. Meets, but flagged for dissent.
- **Research:** Modal 3 vs. P expectation of 3. Meets (partial coverage).
- **Systems:** Modal 2 vs. P expectation of 3. **Below.** This corroborates Alex's HM screen concern.
- **AI Fluency:** Modal 3 vs. P expectation of 3. Meets (partial coverage).
- **Ownership:** Modal 3 vs. P expectation of 3. Meets.

### Risks & Open Questions

- Systems & Platform Thinking is below the P bar (modal 2) with only partial coverage. Alex's HM-screen concern is the strongest signal here, and the take-home and portfolio rounds did not probe systems articulation directly.
- AI Fluency rated only in one round. We are extrapolating from a single point.

### Hiring Recommendation

**Recommendation:** lean no — **Confidence:** medium

**Driving competencies and rounds:**
- Systems & Platform Thinking — modal 2 across HM screen (Alex) and take-home (Priya), below P expectation of 3. Alex's concern corroborated by Priya's take-home rating.
- Craft dissent (3 vs. 4 vs. 2) is unresolved and tied to the same systems-articulation concern.

**The debrief needs to decide:** decline, OR escalate to a follow-up live Figma session targeting systems articulation if the team wants to give the candidate one more chance. Recommend declining unless the team is willing to fund the additional round.

### Debrief Meeting Agenda

| Block | Duration | Focus |
|-------|----------|-------|
| Candidate snapshot | 1 min | P-level product designer; B2B growth surface |
| Dissent first | 10 min | Craft 2 vs. 4; systems articulation question |
| Consensus areas | 5 min | Product, Ownership both modal 3 — confirm |
| Risks & gaps | 5 min | Systems below P bar; AI Fluency under-covered |
| Recommendation read-out | 3 min | Lean no, medium confidence |
| Decision | 5 min | Decline or fund one more round? |

**Anti-groupthink prompt:**
> "Before we decline: who in the loop saw something positive that the systems concern might be overshadowing? What's the strongest case for fund-one-more-round?"
