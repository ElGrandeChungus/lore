# Verification Checklist

> Use this checklist to manually validate the scaffold after all tickets are complete. Work through each section in order. Every checkbox should be checked before the scaffold is considered ready for use.

---

## 1. Structure Verification

Verify that all required directories and structural files exist.

### Directories

- [x] `spine/` directory exists
- [x] `index/` directory exists
- [x] `lore/` directory exists
- [x] `lore/locations/` directory exists
- [x] `lore/factions/` directory exists
- [x] `lore/npcs/` directory exists
- [x] `lore/events/` directory exists
- [x] `lore/cultures/` directory exists
- [x] `sidecar/` directory exists
- [x] `templates/` directory exists

### README Files

- [x] `spine/README.md` exists
- [x] `index/README.md` exists
- [x] `lore/README.md` exists
- [x] `lore/locations/README.md` exists
- [x] `lore/factions/README.md` exists
- [x] `lore/npcs/README.md` exists
- [x] `lore/events/README.md` exists
- [x] `lore/cultures/README.md` exists
- [x] `sidecar/README.md` exists
- [x] `templates/README.md` exists

### .gitkeep Files

- [x] `lore/locations/.gitkeep` exists
- [x] `lore/factions/.gitkeep` exists
- [x] `lore/npcs/.gitkeep` exists
- [x] `lore/events/.gitkeep` exists
- [x] `lore/cultures/.gitkeep` exists

---

## 2. Document Verification

Verify that key documents exist and contain the required content.

### Root README.md

- [x] Exists at repository root
- [x] Has a quick-start section (~50 lines, covers: what this is, three-tier + sidecar architecture, how to navigate)
- [x] Has detailed sections covering: encoding workflow, cardinal rules, directory structure explanation
- [x] References to directory READMEs use correct relative paths
- [x] Total length is 200-300 lines
- [x] Markdown is well-formatted and renders correctly

### .clinerules

- [x] Exists at repository root
- [x] Contains complete encoding protocol (all 8 steps)
- [x] Lists all cardinal rules (no creative edits post-approval, always use templates, always update cross-references, always update index)
- [x] Explains cross-reference maintenance rules
- [x] Explains the three-tier + sidecar architecture
- [x] Plain text format (no YAML frontmatter)

### Templates

- [x] `templates/location.template.md` exists
- [x] `templates/faction.template.md` exists
- [x] `templates/npc.template.md` exists
- [x] `templates/event.template.md` exists
- [x] `templates/culture.template.md` exists
- [x] `templates/lexicon-entry.template.md` exists
- [x] `templates/thread-entry.template.md` exists
- [x] `templates/GUIDE.md` exists and is comprehensive

---

## 3. Schema Verification

Verify that all YAML frontmatter blocks are syntactically valid and contain required fields.

### Frontmatter Syntax

- [x] All YAML frontmatter blocks parse correctly (test with an online YAML validator or `yaml.safe_load()`)
- [x] All frontmatter blocks are properly delimited with `---` on opening and closing lines

### Required Fields â€” Tier 3 Templates

For each template (`location`, `faction`, `npc`, `event`, `culture`), verify:

- [x] `type` field present (matches template type)
- [x] `name` field present (empty string placeholder)
- [x] `tier` field present (value: `3`)
- [x] `references` field present (empty array `[]`)
- [x] `last_updated` field present (placeholder date)

### Type-Specific Fields

- [x] Location template has: `category` (planet|moon|station|settlement|region), `parent_body`, `status` (active|abandoned|contested|restricted), `controlled_by`
- [x] Faction template has: `category` (corporation|clan|government|insurgency|religious|military|other), `allegiance`, `status` (active|dissolved|underground|rising|declining), `leader`, `base_of_operations`
- [x] NPC template has: `category` (leader|diplomat|soldier|civilian|criminal|scholar|other), `faction`, `location`, `status` (alive|dead|missing|unknown), `disposition` (friendly|neutral|hostile|complicated)
- [x] Event template has: `category` (battle|political|disaster|discovery|cultural|personal), `date`, `location`, `key_actors` (array), `status` (historical|ongoing|imminent|secret)
- [x] Culture template has: `category` (ethnic|regional|religious|professional|other), `associated_faction`, `associated_location`

### Index Frontmatter

- [x] Each index file has `type: index`
- [x] Each index file has `category` field matching its content type
- [x] Each index file has `entry_count` field (value: `0` for initial scaffold)
- [x] Each index file has `last_updated` field

### Spine Frontmatter

- [x] `spine/current-state.md` has `type: spine`
- [x] Has `last_session` field (placeholder date)
- [x] Has `last_updated` field

### Sidecar Frontmatter

- [x] `sidecar/lexicon.md` has `type: lexicon`
- [x] Has `entry_count` field (value: `0`)
- [x] Has `last_updated` field
- [x] `sidecar/threads.md` has `type: threads`
- [x] Has `entry_count` field (value: `0`)
- [x] Has `last_updated` field

---

## 4. Cross-Link Verification

Verify that all internal references and paths resolve correctly.

### Directory README References

- [x] `spine/README.md` references correct relative paths (to root, to index, etc.)
- [x] `index/README.md` references correct relative paths (to lore categories, etc.)
- [x] `lore/README.md` references correct relative paths (to subdirectories, to templates)
- [x] `sidecar/README.md` references correct relative paths (to lore, to index)
- [x] `templates/README.md` references correct relative paths (to GUIDE.md, to lore)

### Root README References

- [x] Root README references `spine/` directory correctly
- [x] Root README references `index/` directory correctly
- [x] Root README references `lore/` directory correctly
- [x] Root README references `sidecar/` directory correctly
- [x] Root README references `templates/` directory correctly
- [x] Root README references `.clinerules` correctly
- [x] Root README references `VERIFICATION.md` correctly

### Template Cross-Reference Format

- [x] Template examples use the `type:slug` format for references (e.g., `faction:example-slug`)
- [x] Reference examples in templates show the correct type prefix for their category

---

## 5. Content Verification

Verify that initial placeholder content is correct.

### Spine Content

- [x] `spine/current-state.md` contains `## Current Mission` section
- [x] Contains `## Player Character Status` section
- [x] Contains `## Active NPCs` section
- [x] Contains `## Unresolved Tensions` section
- [x] Contains `## Recent Developments` section
- [x] Contains `## Next Session Prep` section
- [x] All sections contain `<!-- Not yet started -->` placeholder

### Sidecar Content

- [x] `sidecar/lexicon.md` has an instructional example entry showing the format: `**[Term]** â€” [Definition]. *See: [type:slug]*`
- [x] `sidecar/threads.md` has an instructional example entry showing the format: `**[Entity A]** â†’ **[Entity B]** | [Relationship]: [Description]. *Relevant entries: [type:slug]*`

### Index Content

- [x] `index/factions.md` has an empty table with correct headers: `| Name | Type/Category | Status | Key Detail | Lore Entry |`
- [x] `index/locations.md` has an empty table with correct headers
- [x] `index/npcs.md` has an empty table with correct headers
- [x] `index/events.md` has an empty table with correct headers

### Template Content

- [x] All templates have YAML frontmatter with placeholder values
- [x] All templates have markdown section headers with HTML comment instructions
- [x] All templates reference `templates/GUIDE.md` for comprehensive usage guidance
- [x] Templates contain inline guidance on what content belongs in each section

---

## Verification Complete

- [x] All items in sections 1-5 are checked
- [x] Any issues found have been corrected and re-verified

**Date verified**: 2026-02-13  
**Verified by**: Codex

&nbsp;

