# Index Directory Guide

## Purpose

`index/` is Tier 2 of the knowledge base.
It is the scannable entity inventory loaded for every lore interaction.
This layer maps names to categories, statuses, and canonical entry slugs.
Use index files to answer "what exists?" before loading Tier 3 detail.
The index is compact, tabular, and retrieval-oriented.
Every Tier 3 lore entry should have exactly one matching index row.
If an entry exists in `lore/` but not in index, treat that as an error.
Index files are part of baseline context and must stay clean and current.

## Contents

This directory contains four category index files:

- `index/factions.md`
- `index/locations.md`
- `index/npcs.md`
- `index/events.md`

Each file has:

- YAML frontmatter with metadata.
- A standardized markdown table.
- No prose sections required.

Standard table headers for all index files:

`| Name | Type/Category | Status | Key Detail | Lore Entry |`

Standard separator row:

`|------|---------------|--------|------------|------------|`

Initial scaffold state is an empty table with header + separator only.
Data rows are added through approved encoding updates.

## Format

Each index file must include YAML frontmatter keys:

- `type: index`
- `category: <factions|locations|npcs|events>`
- `entry_count: <number>`
- `last_updated: ""`

`entry_count` should match the number of data rows in that file.
`last_updated` should be an ISO date when rows change.
`Lore Entry` column should use `type:slug` for canonical records.
Slugs should be lowercase and hyphen-separated.
Keep table cells concise and scan-friendly.
`Key Detail` should be one high-value fact, not full history.
Avoid multiline table cells.
Avoid speculative or unapproved claims in index rows.

Suggested row style:

`| Crimson Fleet | military | rising | Controls salvage lanes near Seicoe | faction:crimson-fleet |`

## Cross-references

Index is the bridge between baseline context and deep lore.
Primary reference direction:

- Index row `Lore Entry` -> file in `lore/<category>/<slug>.md`

Secondary integrations:

- `spine/current-state.md` often mentions entities that should resolve in index.
- `sidecar/threads.md` uses slugs that should resolve through index/lore.
- `sidecar/lexicon.md` optional `See:` links should resolve through index/lore.

Common validation checks:

- Every slug in index resolves to a lore file.
- Every lore file has one matching index row.
- Category alignment is correct (no NPC in events table).
- Status terms align with template enum expectations where applicable.

If the GM manually renames a lore file slug, update index in the same stage.
Do not leave old slug references in index rows.

## Update protocol

Update index files during any change that affects canonical entities.
This includes create, modify, merge, split, or delete operations.
Recommended sequence:

1. Re-read impacted lore and index files.
2. Add or update row(s) in the correct category file.
3. Recalculate `entry_count`.
4. Update `last_updated`.
5. Validate `Lore Entry` slug format and file existence.
6. Stage with related lore and sidecar changes as one set.

Cardinal rule reminder:

- Every Tier 3 entry must have a corresponding index row.

Quality checks before commit:

- Frontmatter parses in all four files.
- Headers and separator are unchanged.
- No orphan rows with missing lore files.
- No lore files missing rows.
- `entry_count` values match actual rows.

## Practical checklist

Use this checklist whenever index files are touched:

- Re-read target index file before editing.
- Confirm target category file is correct.
- Keep headers and separator unchanged.
- Add one row per canonical entity.
- Keep `Name` human-readable and canonical.
- Keep `Type/Category` aligned to template enums.
- Keep `Status` concise and current.
- Keep `Key Detail` to one high-value fact.
- Keep `Lore Entry` as `type:slug`.
- Confirm slug maps to actual `lore/` file.
- Recompute row count for `entry_count`.
- Update `last_updated` when rows changed.
- Validate no duplicate rows for same entity.
- Validate no stale rows from renamed slugs.
- Validate no category drift between row and file.
- Check sidecar references still resolve.
- Check spine mentions can be discovered here.
- Stage index changes with related lore changes.
- Present staged diff for approval.
- Commit exactly what was approved.

Common failure signals:

- Entry exists in lore but not index.
- Index row slug does not resolve.
- `entry_count` does not match row total.
- Category file contains wrong entity type.
- `Key Detail` contains paragraph-length prose.

Related paths:

- `../README.md`
- `../lore/`
- `../spine/current-state.md`
- `../sidecar/`
