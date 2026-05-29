---
name: team-progress-update
description: "Compose audience-aware team progress updates for design managers in two modes: a weekly team digest (Friday-style recap of what the team shipped, recognition-forward, for the team and adjacent partners) and an exec readout (strategic summary for design VP / product VP / leadership focused on progress vs. OKRs, decisions made, and decisions needed). Use for weekly digests, leadership updates, QBR readouts, VP updates, all-hands recaps, and cross-functional status summaries. Not for 1:1 prep (use `$one-on-one-agenda-automator`) or OKR tracking on a single report (use `$report-objective-tracker`)."
---

# Team Progress Update

## Overview

Use this skill to compose audience-aware team progress updates for design managers. Accepts a mode (weekly digest or exec readout), the team and time window, and produces a structured update built from a scan of Notion / project trackers / `$report-objective-tracker` output. The two modes share ~90% of the input pipeline; they differ in audience framing, section ordering, and what gets emphasized vs. cut.

This skill is not a generic status report — it tailors the voice and shape of the output to the audience. A **weekly digest** is people-first, names the designers behind every ship, leads with recognition, and is written for the team itself and adjacent partners. An **exec readout** is outcome-first, maps work to OKRs, leads with the punch line, and surfaces decisions needed for leaders who need to act, not browse.

Output is formatted for use in Notion, Slack, email, or Google Docs. When the target tool is specified, adapt the formatting accordingly (Slack-friendly bullets and emoji for digests; clean Notion/Docs structure for exec readouts).

## Workflow

1. Establish context.
- Identify the **mode**: `digest` (weekly team-facing) or `exec-readout` (upward, leadership-facing). If the request is ambiguous, ask — see `references/output-modes.md` for the mode-selection decision tree.
- Identify the team (manager, team name, designers in scope).
- Identify the **time window**:
  - Digest default: last 7 days.
  - Exec readout default: last 4 weeks, or "since last readout" if a prior readout date is provided.
- Identify the **audience** explicitly: who is reading this, and what decision or action does it support?
- Note the upcoming event motivating the update (QBR, all-hands, VP review, weekly cadence).

2. Scan sources.
- Reuse the Notion scanning protocol from `../one-on-one-agenda-automator/references/notion-scanning-guide.md` — the shared-pages, assigned-items, and project-tracker queries apply directly. Extend per `references/source-scanning-guide.md`:
  - **Shipped artifacts:** items where status transitioned to Done / Shipped / Launched within the window.
  - **In-flight work:** items in progress with milestones inside the window or the next two weeks.
  - **Blocked / at-risk items:** explicit status flags plus items overdue with no completion signal.
  - **Decisions logged:** scan shared pages for `Decision:` headings, decision-log databases, or pages tagged `decision`.
  - **Open threads:** unresolved comment threads on shared design pages with cross-functional partners.
  - **OKR alignment (exec mode):** pull progress from `$report-objective-tracker` output when provided; otherwise mark OKR mapping as unavailable rather than inventing it.
- Other sources (Linear, Jira, Figma, GitHub) are accepted as direct manager input but are not scanned via MCP.

3. Categorize findings.
- Sort scanned items into the canonical buckets defined in `references/output-modes.md`:
  - Shipped
  - In flight
  - Decisions made
  - Decisions needed
  - Risks / blockers
  - Recognition candidates
  - Coming up / next
- Tag each item with the designer(s), the project, and a link to the Notion artifact.

4. Apply mode-specific framing.
- **Digest mode:** lead with recognition, name designers for every ship, write in plain conversational language, optimize for scannability (bullets, short lines, emoji acceptable). Cut exec-only sections (no OKR roll-up, lighter on "decisions needed").
- **Exec readout mode:** lead with a one-line headline that states the punch line (not "here's our update"). Map the top items to OKRs from `$report-objective-tracker`. Be explicit about red/yellow/green. Make `Decisions Needed` concrete: each decision has an owner, a deadline, and the cost of not deciding. Cut team-internal recognition that doesn't carry strategic weight.

5. Format output.
- Use `references/weekly-digest-template.md` for digest mode.
- Use `references/exec-readout-template.md` for exec readout mode.
- Carry forward open items from any prior update provided (don't silently re-list them — mark them as "carried from [prior date]").

## Output Contract

The two modes have different contracts. Use the contract that matches the requested mode.

**Digest mode** — return sections in this order:
- `Window`
- `Shipped This Week`
- `In Flight`
- `Recognition`
- `Risks & Asks`
- `Coming Up`

**Exec readout mode** — return sections in this order:
- `Headline`
- `Progress vs. OKRs`
- `Decisions Made`
- `Decisions Needed`
- `Risks & Mitigations`
- `Asks`

## Quality Bar

Revise before finalizing if any of these are true:
- Any shipped item omits the designer(s) responsible or omits a link to the artifact.
- Recognition section in digest mode is generic ("great work everyone this week") instead of naming specific people for specific work.
- Exec readout `Headline` describes the document ("Q2 design update") instead of stating the punch line ("Checkout shipped on time; Dashboard v2 is at risk and we need a scope decision by Friday").
- Exec readout does not map the top items to OKRs from `$report-objective-tracker`, and also does not explicitly flag that no OKR source was provided.
- Status is uniformly green — readouts and digests that show 100% green with no risks are too superficial. Re-examine.
- Exec readout `Decisions Needed` is missing, empty, or vague. Each decision must name the decision, the owner, the deadline, and the cost of not deciding.
- Any claim ("project is going well", "we're on track") is not backed by a specific shipped artifact, metric, or status.
- Time window is not stated, or items outside the window are included without being flagged as carry-forward.
- Items carried over from a prior update are silently repeated instead of marked as "carried from [date]".
- Digest mode uses exec-readout framing (OKR roll-ups, decision asks) instead of team-first recognition and ship lists — or vice versa.

## Reference Navigation

Read only what is needed:
- output shells: `references/weekly-digest-template.md`, `references/exec-readout-template.md`
- mode selection and section definitions: `references/output-modes.md`
- source-scanning extensions: `references/source-scanning-guide.md`
- base Notion scanning protocol (shared): `../one-on-one-agenda-automator/references/notion-scanning-guide.md`

## Trigger Examples

Positive:
- "Write our Friday team digest."
- "Generate a weekly recap I can send to the team in Slack."
- "Build the design exec readout for next week's QBR."
- "I need a VP-level update on what design shipped this month."
- "Compose a leadership update — we're presenting to the product VP on Thursday."

Negative:
- "Prep my 1:1 with Sarah." (use `$one-on-one-agenda-automator` — single-report meeting prep)
- "Check progress on Sarah's Q2 objectives." (use `$report-objective-tracker` — single-report OKR tracking)
- "Write objectives for my designer for Q2." (use `$report-objective-creator` — single-report goal setting)
- "Review this candidate's portfolio." (use `$portfolio-reviewer`)

Ambiguous:
- "I need a team update." (clarify: weekly digest for the team, or exec readout for leadership?)
- "Write a status report." (clarify: who is the audience, what decision does it support, and what time window?)
- "Summarize what design did this quarter." (clarify: for the team's all-hands, or for an exec readout?)
