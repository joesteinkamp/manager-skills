# Source Scanning Guide

Extensions to the base Notion scanning protocol for use by `team-progress-update`. Read this in addition to `../one-on-one-agenda-automator/references/notion-scanning-guide.md`, which defines the core queries (shared pages, assigned items, project trackers) reused here unchanged.

## Scope Differences from the 1:1 Scan

| Dimension | 1:1 Scan | Team Progress Update Scan |
|-----------|----------|---------------------------|
| Subject | One report | The whole team (multiple designers) |
| Default window | 7 days | 7 days (digest) / 28 days (exec readout) |
| Primary use | Coaching prompts | Aggregation, attribution, OKR roll-up |
| Output unit | Discussion prompts | Categorized ship list + decisions |

For each designer on the team, run the same per-person scan defined in the base guide, then aggregate.

## Additional Queries

### 1. Shipped Artifacts

**Query:** Across all project trackers and design-task databases the team uses, fetch items where the status property transitioned to one of `Done`, `Shipped`, `Launched`, `Complete` within the window.

**Extract per item:**
- Item title, URL, project, designer(s) (Assignee/Owner), date completed.
- Linked Figma file or spec page if referenced in the item.
- Linked PR / launch announcement if present.

**Signal:**
- High-effort items (multi-week, multi-person) → flag as recognition candidates.
- Items that close out a milestone → flag as OKR-relevant for exec mode.

### 2. Decision Extraction

**Query:** Across pages the team owns or has edited in the window:
- Scan for headings matching `Decision`, `Decisions`, `Decision Log`, or pages tagged `decision`.
- Scan for callout blocks or quote blocks beginning with `Decision:` or `Decided:`.
- If a `Decisions` database exists, query for entries created or updated in the window.

**Extract per decision:**
- Decision statement (one sentence).
- Owner / decider.
- Date.
- Context link (the page the decision came from).
- Status: `Made` or `Pending`.

**Signal:**
- `Pending` decisions older than 7 days → escalate into `Decisions Needed` (exec mode) or `Risks & Asks` (digest mode).
- Made decisions that change a previously communicated direction → flag for the exec headline.

### 3. OKR Cross-Reference (Exec Mode Only)

**Input:** Output from `$report-objective-tracker` for each report on the team, if provided.

**Process:**
- For each shipped item, attempt to match to an objective key result by project name, keyword, or explicit linking in the Notion item.
- For each at-risk item, surface the affected OKR.
- Compute team-level roll-up: count of key results at on-track / needs-attention / at-risk / blocked / achieved.

**Fallback:** If no `$report-objective-tracker` output is provided:
- Do not invent OKR mappings.
- Mark the exec readout's `Progress vs. OKRs` section with an explicit note: "No OKR tracker output provided — items are listed without OKR alignment."

### 4. Carry-Forward from Prior Update

**Input:** A prior digest or exec readout, if provided.

**Process:**
- Extract any `Decisions Needed`, `Asks`, or `Coming Up` items.
- Cross-check against the current scan. If still open, include in the new update with the tag `carried from [prior date]`.
- If now resolved (matching a shipped item or a `Made` decision), surface in `Decisions Made` / `Shipped` and note the resolution.

## Source Coverage

| Source | Scanned via MCP | Accepted as direct input |
|--------|-----------------|--------------------------|
| Notion | ✅ | ✅ |
| Linear | ❌ | ✅ (paste ticket list or export) |
| Jira | ❌ | ✅ |
| Figma | ❌ | ✅ (link to file, manager describes shipped work) |
| GitHub | ❌ | ✅ (PRs merged, links) |
| `$report-objective-tracker` output | N/A (skill output) | ✅ |

If a non-Notion source is the team's primary system of record, request the input explicitly rather than guessing.

## Fallback: No Notion Access

If Notion scanning is unavailable:
1. Note in the update's context that Notion was not scanned.
2. Ask the manager for: list of shipped items (with designers), list of in-flight items, any decisions made or pending, any blockers.
3. Generate the update from the manual input only — do not infer items.
4. For exec readout mode, request OKR tracker output explicitly.

## Aggregation Output Shape (Internal)

Before formatting, the scan produces a structured intermediate the templates consume:

```
team:
  manager: Jordan
  designers: [Sarah, Alex, Priya]
  window: 2026-05-17 to 2026-05-24
shipped:
  - { title, designer, project, date, link, okr? }
in_flight:
  - { title, designer, project, status, due, link }
decisions_made:
  - { decision, owner, date, context_link }
decisions_needed:
  - { decision, owner, deadline, cost_of_delay, context_link }
risks:
  - { item, designer, project, status, signal, link }
recognition_candidates:
  - { item, designer, why }
coming_up:
  - { item, designer, project, due }
carried_forward:
  - { item, from_date, type }
```
