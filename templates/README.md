# Templates Directory Guide

This directory contains structural blueprints for creating entries in the Taito System knowledge base.
Templates enforce consistent schema, section layout, and cross-reference conventions.
They are used during encoding workflows and are not loaded as query context.

## Purpose

- Standardize Tier 3 lore entry structure across all categories.
- Provide inline writing guidance so entries can be drafted quickly and consistently.
- Keep YAML frontmatter machine-parseable while preserving human-readable authoring.
- Reduce schema drift across manual and AI-assisted edits.

## How to Use Templates

1. Classify the new canon item by type.
2. Copy the matching template into the target directory under `lore/`.
3. Replace placeholder values in YAML frontmatter.
4. Fill each markdown section following inline HTML guidance comments.
5. Add `type:slug` references for related entities.
6. Update relevant index files and sidecar files in the same change set.

## Available Templates

- `location.template.md`: Places (planet, moon, station, settlement, region).
- `faction.template.md`: Organizations with goals, power, and continuity.
- `npc.template.md`: Individuals with recurring setting relevance.
- `event.template.md`: Incidents with meaningful consequences.
- `culture.template.md`: Shared social systems and identity frameworks.
- `lexicon-entry.template.md`: Inline pattern for short vocabulary entries in `sidecar/lexicon.md`.
- `thread-entry.template.md`: Inline pattern for campaign relationship entries in `sidecar/threads.md`.

## Classification Rubric

Use this quick decision map when a new canon item is ambiguous.

- If it is a place where scenes happen: `location`.
- If it is a coordinated group with agency: `faction`.
- If it is a named person with recurring impact: `npc`.
- If it is a happening anchored in time: `event`.
- If it is a values/practices system shared by a group: `culture`.
- If it is only a term definition (no depth needed): lexicon inline entry.
- If it is a campaign-only connection between entities: thread inline entry.

## Cross-Reference Rules

- References use `type:slug`, for example `faction:crimson-fleet`.
- Use lowercase, hyphen-separated slugs.
- Keep references bidirectional when canonically justified.
- Confirm referenced slugs resolve to actual entries.

## Authoring Standards

- Keep factual tone and avoid unresolved speculative language in canon sections.
- Use concise paragraphs and scannable bullets.
- Preserve frontmatter key order from template unless there is a strong reason to change it.
- Use ISO dates (`YYYY-MM-DD`) for `last_updated`.
- Keep references current whenever entities are created, merged, or renamed.

## More Detailed Guidance

For full schema details, examples, edge cases, and quality checks, read `templates/GUIDE.md`.

## Related Paths

- Lore destination files: `lore/locations/`, `lore/factions/`, `lore/npcs/`, `lore/events/`, `lore/cultures/`
- Index files: `index/factions.md`, `index/locations.md`, `index/npcs.md`, `index/events.md`
- Sidecar files: `sidecar/lexicon.md`, `sidecar/threads.md`

From this directory, relative links are:

- `GUIDE.md`
- `../lore/`
- `../index/`
- `../sidecar/`
