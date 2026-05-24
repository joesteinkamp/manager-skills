# Exec Readout Template

Use this as the default response structure for `team-progress-update` in `exec-readout` mode. Optimized for a leader (design VP, product VP, cross-functional head) who needs to act, not browse.

## Headline

One line. State the punch line, not the document. The reader should know after this line whether they need to read further and what they need to decide.

> Example: "Checkout shipped on time and is meeting the conversion target. Dashboard v2 is at risk on timeline — we need a scope decision by Friday to hit the May 15 launch."

**Window:** [Start date] – [End date]
**Team:** [Team name, manager]
**OKR tracker output provided:** (yes / no)

## Progress vs. OKRs

Map work to the team's objectives. Use the canonical status scale from `../../report-objective-tracker/references/progress-rating-guide.md`: 🟢 on track / 🟡 needs attention / 🔴 at risk / ✅ achieved / ⚫ blocked.

| OKR / Key Result | Status | Evidence | Owner |
|------------------|--------|----------|-------|
| [KR statement] | 🟢/🟡/🔴/✅/⚫ | [shipped artifact, metric, or specific in-flight progress with link] | [Designer] |
| [KR statement] | | | |

If no OKR tracker output was provided, replace this section with:
> *No OKR tracker output was provided for this window. Items below are grouped by project instead.*
> Then list shipped + in-flight work by project, with status colors per item.

## Decisions Made

Decisions logged in the window that change direction or commit the team to a path.

- **[Decision statement]** — Made by [decider] on [date]. Context: [one-line why]. → [link]
- **[Decision statement]** — Made by [decider] on [date]. Context: [why]. → [link]

## Decisions Needed

Mandatory and concrete. Each item must name the decision, the owner, the deadline, and the cost of not deciding.

- **[Decision needed]**
  - Owner: [name]
  - Deadline: [date]
  - Cost of not deciding by deadline: [specific impact — e.g., "Dashboard v2 May 15 launch slips by 2+ weeks"]
  - Context: [link]
- **[Decision needed]**
  - Owner: [name]
  - Deadline: [date]
  - Cost of not deciding: [specific impact]
  - Context: [link]

## Risks & Mitigations

For each risk, name what could go wrong, what's being done about it, and what would need to change to escalate.

- 🔴 **[Risk]** — [What's at stake]. Mitigation: [what the team is doing]. Escalation trigger: [the condition under which this needs leadership intervention].
- 🟡 **[Risk]** — [What's at stake]. Mitigation: [action]. Escalation trigger: [condition].

## Asks

What the team needs from the reader specifically. Different from "Decisions Needed" — these are resources, alignment, or air cover.

- [Specific ask] — needed by [date] from [person/team]. Reason: [one-line why].

---

## Starter Example

Below is a concrete exec readout example. Use as a quality reference.

### Headline

> Checkout shipped on May 12 and is hitting the +8% conversion target (currently at +6.4% w/o/w, trending green). Dashboard v2 is 🟡 on timeline — we need a scope decision from Jamie (PM) by May 28 to hold the June 15 launch.

**Window:** 2026-04-26 – 2026-05-24 (4 weeks)
**Team:** Growth Design (manager: Jordan; designers: Sarah, Alex, Priya)
**OKR tracker output provided:** Yes

### Progress vs. OKRs

| OKR / Key Result | Status | Evidence | Owner |
|------------------|--------|----------|-------|
| Lift checkout conversion +8% by end of Q2 | 🟢 | Shipped May 12, +6.4% w/o/w, on pace to +8% by June 15 | Alex |
| Launch Dashboard v2 by June 15 | 🟡 | Personas done, journey map in flight, scope drift on competitive analysis | Sarah |
| Cut onboarding drop-off by 15% by end of Q2 | 🟢 | Empty-state pass shipped; tooltip system ships June 3 | Priya |
| Design system component coverage to 80% | 🟡 | Error-state audit added 14 components to backlog; need eng capacity allocation | Alex |

### Decisions Made

- **Dashboard v2 personas locked to 3 (Power User, New Admin, Trial Evaluator)** — Made by Jordan + Jamie (PM) on May 21. Reduced from 5 to keep launch on June 15. → [Notion link]
- **Checkout error-state coverage added to design system roadmap** — Made by Alex + DS lead on May 19. Slots 14 new components into the Q3 design system plan. → [Notion link]

### Decisions Needed

- **Dashboard v2 competitive analysis scope** — kill it, descope to a 1-page summary, or keep as-is and slip launch
  - Owner: Jamie (PM)
  - Deadline: May 28
  - Cost of not deciding: June 15 launch slips by 2+ weeks; Sarah blocked on persona-to-flow work
  - Context: [Notion link to research brief]
- **Design system eng capacity for the 14 new error-state components**
  - Owner: Eng director (Riya)
  - Deadline: June 3
  - Cost of not deciding: Components ship to design but not to production; checkout team has to rebuild error states inline for the next launch
  - Context: [Notion link to DS roadmap]

### Risks & Mitigations

- 🟡 **Dashboard v2 scope drift** — Competitive analysis ballooned from 1 page to a 12-page deep-dive request. Mitigation: Sarah meeting with research May 27 to propose a 1-page version. Escalation trigger: If PM rejects descope, we will need to slip the June 15 launch — flag to product VP that week.
- 🟢 **Checkout conversion lift below target by June 15** — Currently trending green (+6.4%/wk, target +8%). Mitigation: Alex shipping a follow-up A/B test May 30 if pace slows. Escalation trigger: Two consecutive weeks below +1.5%/wk.

### Asks

- Air cover with Jamie (PM) on the Dashboard v2 scope decision — needed by **May 28**. Reason: This is a third escalation; manager-to-PM conversation has stalled twice.
- One eng resource (0.5 FTE for 4 weeks) for the design system error-state components — needed by **June 3** from Eng director (Riya). Reason: Without it, the components don't ship to prod and the next checkout launch reimplements them.
