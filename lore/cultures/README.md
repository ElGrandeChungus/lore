# Cultures Category Guide

## Purpose

`lore/cultures/` stores canonical shared social systems.
Use this category for values, norms, language practices, rituals, and identity frameworks.
A culture entry describes how groups make meaning and coordinate behavior.
Cultures can be regional, religious, professional, ethnic, or mixed.
If shared practice affects choices across many entities, it belongs here.
Do not use this category for command organizations or single individuals.

## Contents

Expected files in this directory:

- `lore/cultures/README.md`: category usage guide.
- `lore/cultures/.gitkeep`: scaffold placeholder.
- `lore/cultures/<slug>.md`: canonical culture entries.

Use the matching template:

- `templates/culture.template.md`

Culture frontmatter fields include:

- `type`, `name`, `tier`, `category`
- `associated_faction`, `associated_location`
- `references`, `last_updated`

Required body sections:

- Overview
- Values & Beliefs
- Language & Communication
- Social Structure
- Aesthetic & Material Culture
- Relationship to Power
- Notes

## Format

Always start from `templates/culture.template.md`.
Category enum values:

- `ethnic`
- `regional`
- `religious`
- `professional`
- `other`

`associated_faction` should use `faction:<slug>` when relevant.
`associated_location` should use `location:<slug>` when anchored to place.
Focus on shared patterns, not one-off anecdotes.
Use concrete examples that affect missions or negotiations.
Keep prose concise and scannable.
Use `Notes` for unresolved interpretations or pending confirmation.

Well-formed entry examples:

- `lore/cultures/daysail-nomads.md`
- `lore/cultures/dock-rites-collective.md`

## Cross-references

Common outbound references from cultures:

- Institutional anchors -> `faction:<slug>`
- Geographic anchors -> `location:<slug>`
- Influential incidents -> `event:<slug>`
- Representative individuals -> `npc:<slug>`

Common inbound references to cultures:

- Faction cultural identity sections
- Location significance/history sections
- Event context/consequence sections
- Lexicon terminology definitions

Cross-reference patterns to validate:

- If culture is tied to faction, faction should acknowledge it.
- If culture is place-bound, location should reference social presence.
- If event reshapes norms, both event and culture should cross-link.

## Update protocol

Update culture entries when shared norms or identity conditions change.
Typical triggers:

- Migration shifts identity boundaries.
- Institutional pressure alters practice.
- Ritual changes become widely adopted.
- Language shifts affect diplomacy or command.

Classification edge cases:

- Militia tradition:
Use culture for the norm system.
Use faction for the armed organization.

- Corporate etiquette manual:
Use culture if practice extends beyond one org chart.
Use faction if internal policy is the core.

- Named priest with followers:
Use NPC for person.
Use culture for doctrine/practice community.

Update sequence:

1. Re-read culture and linked entities.
2. Edit using template section integrity.
3. Add/update references and validate slugs.
4. If needed, add lexicon terms for key vocabulary.
5. Stage and request approval.

Quality checks:

- Frontmatter parses and enums are valid.
- Associated faction/location fields are coherent.
- Claims describe shared patterns, not isolated behavior.
- References resolve and support retrieval.

Practical checks:

- Category enum is exact.
- Associated fields resolve when present.
- Beliefs and practices are socially distributed.
- Power relationship section includes tension points.
- Language markers are usable at the table.
- Cross-links to factions/locations are current.
- Index and lexicon implications are considered.
- Major internal variation is documented when canonically relevant.
- Culture claims avoid overgeneralizing every member.
- Event links reflect meaningful cultural change points.
- Notes call out unresolved interpretation risks.
- Terminology aligns with lexicon definitions when available.
