# Lore Directory Guide

## Purpose

`lore/` is Tier 3 of the knowledge base.
It stores deep canonical entries for world entities.
This is the authoritative truth layer for reusable setting content.
Unlike spine and threads, lore is campaign-agnostic by default.
Lore should survive campaign resets unless canon is intentionally revised.
Entries in this directory are loaded on demand, not in bulk.
Use lore when a query requires depth, history, or cross-entity context.
Keep each entry scoped to one primary entity type.

## Contents

This directory contains category subdirectories:

- `lore/locations/`
- `lore/factions/`
- `lore/npcs/`
- `lore/events/`
- `lore/cultures/`

Each subdirectory has:

- A category README with classification and usage guidance.
- A `.gitkeep` for scaffold continuity.
- Canonical entry files as markdown with YAML frontmatter.

Entry naming convention:

- File name should match slug: `<slug>.md`
- Slug format: lowercase, hyphen-separated.
- Example: `lore/factions/crimson-fleet.md`

Do not store templates in `lore/`; use `templates/` for creation blueprints.
Do not store session-only relationship notes here; use `sidecar/threads.md`.

## Format

All lore entries use YAML frontmatter plus sectioned markdown body.
Base required frontmatter keys for Tier 3:

- `type`
- `name`
- `tier: 3`
- `references: []`
- `last_updated`

Type-specific fields are defined in template files:

- `templates/location.template.md`
- `templates/faction.template.md`
- `templates/npc.template.md`
- `templates/event.template.md`
- `templates/culture.template.md`

Creation rule:

- Every new lore entry must start from the matching template.

Style rules:

- Keep factual tone.
- Prefer structured bullets for discrete facts.
- Move uncertainty to `Notes`.
- Keep references explicit with `type:slug`.

## Cross-references

Lore entries are a reference graph, not isolated pages.
Common link patterns:

- `location` <-> `faction` (control, bases, claims)
- `npc` <-> `faction` (leadership, affiliation, conflict)
- `event` <-> `location` (where it happened)
- `event` <-> `npc`/`faction` (key actors)
- `culture` <-> `location`/`faction` (association and pressure)

Resolution path:

1. Parse `type:slug`.
2. Confirm in category index file.
3. Load corresponding lore file.

Keep references bidirectional when canonically justified.
If bidirectional symmetry is not valid, explain asymmetry in text.
Avoid dangling references to non-existent slugs.

Integration with other layers:

- Index provides discoverability and path resolution.
- Spine summarizes only active slices of lore.
- Sidecar threads connect campaign arcs to stable lore.
- Lexicon may point to lore terms needing deeper context.

## Update protocol

Update lore through encoding or approved maintenance operations.
Recommended process:

1. Classify entity type.
2. Start from matching template.
3. Fill frontmatter and sections.
4. Add cross-references.
5. Update matching index row(s).
6. Update sidecar entries if campaign context changes.
7. Re-read all impacted files before staging.
8. Stage for GM approval and commit exactly approved content.

On-demand loading guidance:

- Do not load all lore files for normal query flow.
- Load only entries relevant to the user question.
- Follow references selectively as needed.

Quality checks before commit:

- Frontmatter parses.
- Template-required sections exist.
- Slug matches file name.
- Index row exists and is accurate.
- References resolve.

Related paths:

- `../README.md`
- `../templates/`
- `../index/`
- `../sidecar/`
- `./locations/`, `./factions/`, `./npcs/`, `./events/`, `./cultures/`

## Practical checklist

Before creating or modifying lore entries:

- Confirm the correct category directory.
- Start from the matching template file.
- Keep required frontmatter keys intact.
- Keep section headings template-consistent.
- Add references only to real entities.
- Validate reference slugs through index.
- Update matching index row in same stage.
- Update sidecar terms/threads when relevant.
- Re-read all impacted files before staging.
- Keep notes operational, not canonical core.
- Keep prose concise and evidence-oriented.
- Confirm no unresolved placeholders remain.
- Stage for GM review and approval.
- Commit exactly staged content.
