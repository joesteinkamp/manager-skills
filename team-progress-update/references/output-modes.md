# Output Modes

Reference for the two canonical modes this skill produces. Use this to select the right mode and shape the right output.

## Mode Comparison

| Dimension | Weekly Digest | Exec Readout |
|-----------|---------------|--------------|
| Audience | The team itself + adjacent partners (PMs, eng leads who sit next to the team) | Design VP, product VP, cross-functional leadership |
| Cadence | Weekly (typically Friday) | Monthly, biweekly, or event-driven (QBR, VP review) |
| Default window | Last 7 days | Last 4 weeks, or "since last readout" |
| Goal | Maintain shared context, recognize work, surface near-term risks and next steps | Inform a leadership decision or unblock a strategic ask |
| Voice | Conversational, plain language, people-first | Tight, outcome-first, decision-oriented |
| Leads with | Recognition / what we shipped | A one-line headline that states the punch line |
| Names individuals | Always — every ship is attributed to a designer | Only when relevant to the strategic story |
| OKR mapping | Not required | Required for the top items, or explicitly flagged as unavailable |
| Decisions Needed section | Optional / light | Mandatory and concrete (decision, owner, deadline, cost of not deciding) |
| Status honesty | Mention risks but don't catastrophize | Honest red/yellow/green — uniformly green readouts are too superficial |
| Format target | Slack / email / Notion (scannable, bullets, emoji OK) | Notion / Google Docs / slide narrative (clean, structured) |

## Canonical Buckets

Both modes draw from the same categorized findings, then include or omit them per mode:

- **Shipped** — items transitioned to Done / Shipped / Launched in the window.
- **In flight** — active work with milestones in the window or the next 2 weeks.
- **Decisions made** — decisions logged in shared pages or decision-log databases.
- **Decisions needed** — open decisions blocking progress, with owner and deadline.
- **Risks / blockers** — at-risk items, blocked items, items overdue.
- **Recognition candidates** — high-impact ships, parallel workstream juggling, cross-functional wins.
- **Coming up / next** — milestones, deadlines, launches in the next 2 weeks.

## Mode Selection Decision Tree

Use this when the requested mode is ambiguous.

1. **Who is the primary reader?**
   - The team / immediate partners → `digest`.
   - A leader who is not in the team's daily work (VP, exec, cross-functional head) → `exec-readout`.

2. **What is the cadence?**
   - Weekly or recurring on a fixed day → `digest`.
   - Tied to an event (QBR, VP review, board, all-hands), or monthly/quarterly → `exec-readout`.

3. **What outcome does it support?**
   - Shared context and motivation → `digest`.
   - A decision, a resource ask, or a strategic alignment moment → `exec-readout`.

4. **Two or three signals pointing the same direction → go with that mode. Mixed signals → ask the manager.**

## Section Inclusion by Mode

| Section | Digest | Exec Readout |
|---------|--------|--------------|
| Window / time frame | ✅ | ✅ (in `Headline` line) |
| Shipped This Week | ✅ | Rolled into `Progress vs. OKRs` |
| In Flight | ✅ | Rolled into `Progress vs. OKRs` |
| Recognition | ✅ | ❌ (only if it carries strategic weight) |
| Risks & Asks | ✅ (light) | Split into `Risks & Mitigations` + `Asks` |
| Coming Up | ✅ | Folded into `Decisions Needed` and `Asks` |
| Headline | ❌ | ✅ |
| Progress vs. OKRs | ❌ | ✅ |
| Decisions Made | ❌ (or light) | ✅ |
| Decisions Needed | Optional | ✅ (mandatory) |

## Voice Examples

**Digest — recognition opener:**
> 🎉 Big week. Sarah shipped the Dashboard v2 persona cards two days ahead of schedule, and Alex closed out the checkout error-state audit. Both unblock the next sprint.

**Exec readout — headline opener:**
> Checkout launched on time and is meeting the conversion target. Dashboard v2 is at risk on timeline; we need a scope decision by Friday to hit the May 15 launch.

The digest is for the team and feels human. The exec readout is for a leader and feels like a brief.
