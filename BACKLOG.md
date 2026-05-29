# Skill Backlog

Skill ideas not yet built. Each entry uses the same fields a real `SKILL.md` would need, so an entry can be lifted into a new skill folder with minimal rework.

Status legend: `idea` (captured, not designed) · `spec` (designed, not built) · `built` (lives in the repo).

---

## debrief-synthesizer

**Status:** built (`hiring/debrief-synthesizer/`)

**One-line description:** Convert per-interviewer scorecards and notes from a hiring loop into a hire/no-hire recommendation with dissenting views surfaced.

**Why it matters for a design manager:** Hiring debriefs are time-consuming and easy to get wrong — strong dissenting signals get smoothed over, groupthink wins, and the manager carries the synthesis burden alone. A skill that aggregates and ranks signal by interviewer + competency makes debriefs faster and more honest.

**Key inputs:**
- Per-interviewer scorecards from the existing hiring suite (`$portfolio-reviewer`, `$case-study-evaluation`, `$evaluate-hiring-manager-screen`, `$de-linkedin-profile-evaluation`).
- Loop structure (which rounds, which competencies each round covered).
- Optional: candidate's calibrated level expectation, role rubric.

**Related existing skills:** all of `hiring/` — this is the synthesis layer that sits on top of the per-round evaluation skills. Likely reads `hiring/references/design-competencies.md`.

**Output sketch:** Hire / no-hire recommendation with confidence, competency-by-competency roll-up across the loop, dissenting views explicitly called out, gaps to probe in a follow-up round if undecided.

---

## team-health-pulse

**Status:** idea

**One-line description:** Synthesize themes from recent 1:1 notes and engagement/attrition signals into a team-health snapshot for the manager and for skip-level use.

**Why it matters for a design manager:** Patterns across reports (workload complaints, career stagnation, intra-team friction) are visible only when you zoom out from individual 1:1s. Most managers don't do this zoom-out systematically and miss attrition signals until it's too late.

**Key inputs:**
- Recent outputs from `$one-on-one-agenda-automator` (last 4-8 weeks across reports).
- Recent outputs from `$report-objective-tracker` (where multiple reports are off-track in the same way).
- Optional: engagement survey themes, recent departures, recent hires.

**Related existing skills:** `$one-on-one-agenda-automator`, `$report-objective-tracker`, and the future `$team-progress-update` (could share the team-aggregation scan).

**Output sketch:** Team-level themes (top 3 strengths, top 3 risks), attrition signals (carried-forward concerns, energy dips, career stagnation), recommended manager actions, suggested skip-level talking points.

---

## staffing-allocator

**Status:** idea

**One-line description:** Allocate designers across projects given a roadmap, team capacity, and each report's growth goals.

**Why it matters for a design manager:** Staffing decisions are where strategy meets people development. Done well, they double as career development. Done poorly, they burn out the strong designers and leave the rest stagnant. Most managers do this in their head with a spreadsheet, and the growth-goal dimension gets dropped.

**Key inputs:**
- Roadmap (projects, scope estimates, deadlines).
- Team capacity (designers, levels, current allocations, time off).
- Growth goals per report from `$report-objective-creator` outputs.
- Optional: cross-functional partner preferences, project complexity rubric.

**Related existing skills:** `$report-objective-creator` (growth goals), `$report-objective-tracker` (where current commitments are at risk), the future `$team-progress-update` (current load is visible in the team scan).

**Output sketch:** Per-designer allocation across the period with rationale (delivery fit + growth fit), gaps (projects without designers), overloads (designers over capacity), tradeoffs explicitly named, recommended manager conversations.
