# Factions Category Guide

## Purpose

`lore/factions/` stores canonical organization entries.
Use this category for corporations, clans, governments, insurgencies, and similar groups.
A faction has persistent identity, agency, and goals over time.
Entries here track power structure, motives, capabilities, and relationships.
Faction files should explain who can act at scale and why.
If a group changes campaign dynamics beyond one scene, it belongs here.
Temporary ad hoc crews can remain in event notes unless reused.

## Contents

Expected files in this directory:

- `lore/factions/README.md`: category operating guide.
- `lore/factions/.gitkeep`: scaffold placeholder.
- `lore/factions/<slug>.md`: canonical faction entries.

Use the matching template:

- `templates/faction.template.md`

Faction frontmatter fields include:

- `type`, `name`, `tier`, `category`, `allegiance`
- `status`, `leader`, `base_of_operations`, `references`, `last_updated`

Required body sections:

- Overview
- Structure & Leadership
- Goals & Motivations
- Resources & Capabilities
- Relationships
- Cultural Identity
- History
- Notes

## Format

Always start from `templates/faction.template.md`.
Use file name as canonical slug.
Category enum values:

- `corporation`
- `clan`
- `government`
- `insurgency`
- `religious`
- `military`
- `other`

Status enum values:

- `active`
- `dissolved`
- `underground`
- `rising`
- `declining`

`leader` should reference `npc:<slug>` when applicable.
`base_of_operations` should reference `location:<slug>` when applicable.
Use short paragraphs and structured bullets for capabilities and relationships.
Avoid writing faction lore as character biography or event chronology alone.

Well-formed entry examples:

- `lore/factions/crimson-fleet.md`
- `lore/factions/frontier-assembly.md`

## Cross-references

Common outbound references from factions:

- Leadership -> `npc:<slug>`
- Headquarters/theater -> `location:<slug>`
- Rivalries/alliances -> `faction:<slug>`
- Defining incidents -> `event:<slug>`
- Internal ideology -> `culture:<slug>`

Common inbound references to factions:

- Location `controlled_by`
- NPC `faction`
- Event `key_actors`
- Culture `associated_faction`

Cross-reference patterns to validate:

- If faction leader exists, NPC file should reference faction role.
- If base exists, location file should mention control/presence.
- If rivalry is active, counterpart faction should usually reflect it.

## Update protocol

Update faction entries when leadership, goals, power, or alignment changes.
Typical triggers:

- Leadership transition.
- Schism or merger.
- Capability expansion or collapse.
- Shift in allegiance or strategic doctrine.

Classification edge cases:

- Religious movement with formal command:
Use faction if command and strategy are central.
Use culture if shared belief practice is central.

- Mercenary unit appearing once:
Use event-only mention unless recurring.
Promote to faction when persistent identity emerges.

- City administration:
Use faction for governing institution.
Use location for city as place.

Update sequence:

1. Re-read faction and linked entities.
2. Apply edits with template section integrity.
3. Update `index/factions.md` row and metadata.
4. Sync affected NPC/location/event/culture references.
5. Stage and request approval.

Quality checks:

- Frontmatter parses and enums are valid.
- References resolve through index.
- Goals, capabilities, and relationships are current and non-contradictory.
- Notes remain operational, not canonical core.

Practical checks:

- Category/status values use approved enums.
- Leader and base slugs resolve correctly.
- Relationships are symmetric where appropriate.
- Capabilities are concrete and not inflated.
- History supports current strategic posture.
- Index row mirrors current faction status.

