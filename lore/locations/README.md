# Locations Category Guide

## Purpose

`lore/locations/` stores canonical place entries.
Use this category for planets, moons, stations, settlements, and regions.
A location is any scene-capable place with persistent identity.
Entries here provide geography, control, significance, and local history.
Location files should support mission planning and spatial reasoning.
If a place matters repeatedly, it belongs here.
If a place is one-time and trivial, keep it in session notes instead.

## Contents

Expected files in this directory:

- `lore/locations/README.md`: category rules and examples.
- `lore/locations/.gitkeep`: scaffold placeholder.
- `lore/locations/<slug>.md`: canonical location entries.

Use the matching template:

- `templates/location.template.md`

Location frontmatter fields include:

- `type`, `name`, `tier`, `category`, `parent_body`
- `status`, `controlled_by`, `references`, `last_updated`

Required body sections:

- Physical Description
- Political Status
- Significance
- Key Sites
- History
- Notes

## Format

Always create new files from `templates/location.template.md`.
Keep file names slug-aligned with entity identity.
Use category enum values exactly:

- `planet`
- `moon`
- `station`
- `settlement`
- `region`

Use status enum values exactly:

- `active`
- `abandoned`
- `contested`
- `restricted`

`controlled_by` should be `faction:<slug>`, `disputed`, or `none`.
Use `references` to connect to factions, NPCs, events, and cultures.
Write concise descriptive prose plus scannable bullets.
Place uncertain facts in `Notes` with clear confidence language.

Well-formed entry examples:

- `lore/locations/seicoe-station.md`
- `lore/locations/mirren-basin.md`

Example slug references in body/frontmatter:

- `faction:crimson-fleet`
- `event:battle-of-mirren`
- `npc:commander-voss`

## Cross-references

Common outbound references from locations:

- Controlling factions -> `faction:<slug>`
- Notable residents/leaders -> `npc:<slug>`
- Major incidents -> `event:<slug>`
- Local social systems -> `culture:<slug>`

Common inbound references to locations:

- Faction `base_of_operations`
- NPC `location`
- Event `location`
- Culture `associated_location`

Cross-reference patterns to validate:

- If `controlled_by` is a faction slug, that faction should mention the location.
- If a key event happened here, event file should reference this location.
- If an NPC is anchored here, NPC file should include this location.

## Update protocol

Update location entries when geography, control, or significance changes.
Typical triggers:

- New mission theater introduced.
- Territorial control shifts.
- Discovery of new key site.
- Historical reinterpretation approved as canon.

Classification edge cases:

- Mobile fleet habitat:
Use location if treated as a persistent place.
Use faction for operating authority.

- Temporary battlefield:
Use event if place has no persistent identity.
Promote to location only if repeatedly revisited.

- Institution campus:
Use location for the place.
Use faction for the institution.

Update sequence:

1. Re-read target location and linked entries.
2. Edit location from template structure.
3. Update related index row in `index/locations.md`.
4. Update linked entities if relationships changed.
5. Stage with cross-reference fixes and submit for approval.

Quality checks:

- Frontmatter parses and enums are valid.
- File slug and entity name alignment is reasonable.
- Key references resolve through index.
- Notes do not contain core canon that belongs in main sections.

Practical checks:

- Category and status enums are exact.
- Control claims are traceable to factions.
- Key sites are scene-usable, not vague.
- History explains current status clearly.
- Related event and NPC links are current.
- Index row reflects latest state.

