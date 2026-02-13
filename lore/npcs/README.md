# NPCs Category Guide

## Purpose

`lore/npcs/` stores canonical non-player character entries.
Use this category for named individuals with recurring relevance.
An NPC entry captures role, motives, ties, and actionable leverage.
NPC files should make interaction consequences clear.
If a person can influence future sessions, create an entry here.
One-scene incidental characters usually do not need full canonical files.
Promote incidental characters when they gain durable impact.

## Contents

Expected files in this directory:

- `lore/npcs/README.md`: category guide and rules.
- `lore/npcs/.gitkeep`: scaffold placeholder.
- `lore/npcs/<slug>.md`: canonical NPC entries.

Use the matching template:

- `templates/npc.template.md`

NPC frontmatter fields include:

- `type`, `name`, `tier`, `category`, `faction`
- `location`, `status`, `disposition`, `references`, `last_updated`

Required body sections:

- Appearance & First Impression
- Role & Position
- Personality & Motivation
- Relationships
- Knowledge & Secrets
- Combat Profile
- Notes

## Format

Always start from `templates/npc.template.md`.
Category enum values:

- `leader`
- `diplomat`
- `soldier`
- `civilian`
- `criminal`
- `scholar`
- `other`

Status enum values:

- `alive`
- `dead`
- `missing`
- `unknown`

Disposition enum values:

- `friendly`
- `neutral`
- `hostile`
- `complicated`

`faction` should be `faction:<slug>` if affiliated.
`location` should be `location:<slug>` for current base.
Keep entries actionable: what the NPC wants, knows, and can do.
Avoid purely decorative characterization without campaign impact.

Well-formed entry examples:

- `lore/npcs/commander-voss.md`
- `lore/npcs/lia-sarre.md`

## Cross-references

Common outbound references from NPCs:

- Affiliation -> `faction:<slug>`
- Current base -> `location:<slug>`
- Key relationships -> `npc:<slug>` or `faction:<slug>`
- Involved incidents -> `event:<slug>`

Common inbound references to NPCs:

- Faction `leader`
- Event `key_actors`
- Location notable personnel mentions
- Threads entries for campaign-specific obligations

Cross-reference patterns to validate:

- If NPC leads a faction, faction file should mirror leadership.
- If NPC is tied to major event, event should include NPC in key actors.
- If NPC location changes, update both NPC and affected context entries.

## Update protocol

Update NPC entries when role, status, motives, or relationships change.
Typical triggers:

- Promotion, demotion, defection, capture, death, disappearance.
- Major revelation in knowledge/secrets.
- Shift in disposition toward PCs or key factions.

Classification edge cases:

- Historical figure with no live relevance:
Prefer event mention unless recurring influence exists.

- Anonymous role ("Station Clerk"):
Keep in session notes unless uniquely identifiable and recurring.

- AI collective represented by one persona:
Use NPC for persona if treated as character.
Use faction/culture for broader collective.

Update sequence:

1. Re-read NPC and connected entries.
2. Edit with template section integrity.
3. Update `index/npcs.md` row and metadata.
4. Sync faction/location/event references.
5. Stage and seek approval.

Quality checks:

- Frontmatter parses and enums are valid.
- References resolve.
- Current status and disposition reflect approved canon.
- Secrets section distinguishes known vs hidden information.

Practical checks:

- Category/status/disposition enums are exact.
- Faction and location slugs resolve.
- Role and motive are actionable.
- Relationship section includes current leverage ties.
- Combat profile matches role and resources.
- Index row matches current NPC state.

