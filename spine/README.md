# Spine Directory Guide

## Purpose

`spine/` is Tier 1 of the knowledge base.
It tracks live campaign state in a compact, always-loaded format.
This directory answers "where are we now?" without loading deep lore.
Use it for session continuity, immediate stakes, and short-horizon planning.
Keep this layer lightweight so it fits baseline context budgets.
This directory is campaign-specific and intentionally volatile.
When a campaign resets, this layer is expected to reset.
The canonical file in this directory is `spine/current-state.md`.
All entries here should reflect approved table state, not speculative ideas.
If uncertain facts appear, place them in `Notes` sections elsewhere until confirmed.

## Contents

Files currently expected in this directory:

- `spine/README.md`: this operating guide.
- `spine/current-state.md`: the active campaign state snapshot.

`spine/current-state.md` has six required sections:

1. `## Current Mission`
What the party is trying to accomplish right now.
Include objective, immediate blockers, and success condition.

2. `## Player Character Status`
Operational condition of each PC.
Include injuries, obligations, stressors, and relevant resource status.

3. `## Active NPCs`
Only NPCs currently on-stage or imminent to next play.
List name, role, current position, and pressure they apply.

4. `## Unresolved Tensions`
Conflicts that can trigger scenes soon.
Include political, interpersonal, logistical, or military tensions.

5. `## Recent Developments`
Short summary of what changed most recently.
This section should bridge memory between sessions.

6. `## Next Session Prep`
Actionable prep cues.
Focus on likely scenes, unresolved choices, and needed callbacks.

## Format

`spine/current-state.md` must use YAML frontmatter.
Required keys:

- `type: spine`
- `last_session: ""`
- `last_updated: ""`

After frontmatter, keep the six required markdown sections in fixed order.
Each section can use bullets or short paragraphs.
Prefer concise updates over narrative prose.
Use HTML comment placeholders when no canon exists yet:
`<!-- Not yet started -->`
Use ISO dates (`YYYY-MM-DD`) once dates are known.
Do not add additional top-level sections unless there is a durable need.
If extra detail is required, link to lore entities with `type:slug` references.

## Cross-references

Spine is a summary layer and should point outward to canonical records.
Common reference targets:

- `index/*.md` for quick entity discovery.
- `lore/*/*.md` for deep canonical details.
- `sidecar/threads.md` for campaign-specific active relationships.
- `sidecar/lexicon.md` for recurring terms used in current mission context.

Use type-prefixed slugs in prose when useful:

- `npc:commander-voss`
- `location:seicoe-station`
- `event:battle-of-mirren`

If a spine item references an entity not in the index, flag it during staging.
Do not invent deep canon here to compensate for missing lore entries.
Instead, stage needed lore/index additions in the same change set.

## Update protocol

Update `spine/current-state.md` after every session or major between-session shift.
Use Flow 3 (post-session update) from `traycer_artifacts/specs/Core Flows.md`.
Recommended sequence:

1. Capture changes to mission, PCs, on-stage NPCs, tensions, and developments.
2. Draft updated spine content in all six sections.
3. Bundle implied canon updates by default:
For example, changed NPC status in `lore/npcs/` and `index/npcs.md`.
4. Re-read impacted files before staging (hybrid editing resilience).
5. Stage in hybrid format for GM approval.
6. Commit exactly what was approved.

Maintenance rules:

- Keep spine concise and current.
- Remove stale details that no longer affect play.
- Update `last_updated` whenever file content changes.
- Update `last_session` when a real session date is known.
- Preserve section order for consistent AI retrieval behavior.

Quality checks before commit:

- Frontmatter parses.
- All six sections exist.
- No placeholder remains in sections that now have canon.
- References are valid against index/lore.
- Changes match approved staging text exactly.

Related paths:

- `../README.md`
- `../index/`
- `../sidecar/`
- `current-state.md`

## Practical checklist

Use this quick pass before finalizing any spine update:

- Confirm every section reflects the latest approved canon.
- Remove details that are no longer actionable.
- Ensure NPC names used here exist in `index/npcs.md`.
- Ensure location mentions resolve in `index/locations.md`.
- Ensure mission blockers map to current tensions or threads.
- Keep wording concise and retrieval-friendly.
- Avoid speculative future outcomes in factual sections.
- Move unresolved ambiguity to `Notes` in canonical entries.
- Verify `last_updated` was changed when content changed.
- Verify `last_session` is the actual session date when known.
- Re-open file after edit to catch formatting mistakes.
- Stage with any implied index/lore changes.
- Submit for approval before commit.
