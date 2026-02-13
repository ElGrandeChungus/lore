# Events Category Guide

## Purpose

`lore/events/` stores canonical incidents anchored in time.
Use this category for battles, political shifts, disasters, discoveries, and similar happenings.
An event entry records what happened, why it happened, and what changed.
Events link cause and consequence across locations, factions, and NPCs.
If an incident affects future decisions, it should have an event entry.
Minor scene beats can stay in session notes unless they gain wider impact.

## Contents

Expected files in this directory:

- `lore/events/README.md`: category standards.
- `lore/events/.gitkeep`: scaffold placeholder.
- `lore/events/<slug>.md`: canonical event entries.

Use the matching template:

- `templates/event.template.md`

Event frontmatter fields include:

- `type`, `name`, `tier`, `category`, `date`
- `location`, `key_actors`, `status`, `references`, `last_updated`

Required body sections:

- Summary
- Context
- Key Details
- Consequences
- Open Questions
- Notes

## Format

Always start from `templates/event.template.md`.
Category enum values:

- `battle`
- `political`
- `disaster`
- `discovery`
- `cultural`
- `personal`

Status enum values:

- `historical`
- `ongoing`
- `imminent`
- `secret`

`location` should use `location:<slug>` when known.
`key_actors` should list `npc:<slug>` and/or `faction:<slug>`.
Use concise chronological bullets in `Key Details`.
`Consequences` must include both immediate and ongoing effects where possible.
Do not turn event files into broad faction overviews.

Well-formed entry examples:

- `lore/events/battle-of-mirren.md`
- `lore/events/seicoe-charter-crisis.md`

## Cross-references

Common outbound references from events:

- Where it happened -> `location:<slug>`
- Who acted -> `npc:<slug>`, `faction:<slug>`
- Related prior/subsequent incidents -> `event:<slug>`
- Social implications -> `culture:<slug>`

Common inbound references to events:

- Location history sections
- Faction history sections
- NPC biography and secrets sections
- Spine recent developments summaries

Cross-reference patterns to validate:

- Key actors should usually reference the event in their own entries.
- Major location events should appear in location history.
- Event chains should preserve timeline clarity across linked events.

## Update protocol

Update event entries as facts are confirmed, revised, or declassified.
Typical triggers:

- Ongoing event receives new phase details.
- Secret event becomes public canon.
- Consequences become measurable in later sessions.

Classification edge cases:

- Institutional reform:
Use event for the reform moment.
Use faction for the institution profile.

- Cultural holiday:
Use event for specific festival instance.
Use culture for enduring tradition system.

- Personal duel with geopolitical effects:
Use event if consequences extend beyond individuals.
Keep interpersonal detail in NPC links as needed.

Update sequence:

1. Re-read event and connected files.
2. Edit event with template section integrity.
3. Update `index/events.md` row and metadata.
4. Sync references in linked location/faction/NPC entries.
5. Stage and request approval.

Quality checks:

- Frontmatter parses and enums are valid.
- Date and status are coherent.
- Key actors are slug-valid.
- Consequences are explicit and non-empty.

Practical checks:

- Category and status enums are exact.
- Date field is unambiguous for table use.
- Location and key actors resolve.
- Key details include causal sequence.
- Consequences include both winners and costs.
- Open questions are campaign-relevant.
- Index row reflects current event state.
- Timeline placement is consistent with linked events.
- Secret/ongoing status changes are propagated to related entries.
- Newly resolved questions are removed or rewritten.
