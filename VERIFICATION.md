# Verification Checklist

> Use this checklist to manually validate the scaffold after all tickets are complete. Work through each section in order. Every checkbox should be checked before the scaffold is considered ready for use.

---

## 1. Structure Verification

Verify that all required directories and structural files exist.

### Directories

- [ ] `spine/` directory exists
- [ ] `index/` directory exists
- [ ] `lore/` directory exists
- [ ] `lore/locations/` directory exists
- [ ] `lore/factions/` directory exists
- [ ] `lore/npcs/` directory exists
- [ ] `lore/events/` directory exists
- [ ] `lore/cultures/` directory exists
- [ ] `sidecar/` directory exists
- [ ] `templates/` directory exists

### README Files

- [ ] `spine/README.md` exists
- [ ] `index/README.md` exists
- [ ] `lore/README.md` exists
- [ ] `lore/locations/README.md` exists
- [ ] `lore/factions/README.md` exists
- [ ] `lore/npcs/README.md` exists
- [ ] `lore/events/README.md` exists
- [ ] `lore/cultures/README.md` exists
- [ ] `sidecar/README.md` exists
- [ ] `templates/README.md` exists

### .gitkeep Files

- [ ] `lore/locations/.gitkeep` exists
- [ ] `lore/factions/.gitkeep` exists
- [ ] `lore/npcs/.gitkeep` exists
- [ ] `lore/events/.gitkeep` exists
- [ ] `lore/cultures/.gitkeep` exists

---

## 2. Document Verification

Verify that key documents exist and contain the required content.

### Root README.md

- [ ] Exists at repository root
- [ ] Has a quick-start section (~50 lines, covers: what this is, three-tier + sidecar architecture, how to navigate)
- [ ] Has detailed sections covering: encoding workflow, cardinal rules, directory structure explanation
- [ ] References to directory READMEs use correct relative paths
- [ ] Total length is 200-300 lines
- [ ] Markdown is well-formatted and renders correctly

### .clinerules

- [ ] Exists at repository root
- [ ] Contains complete encoding protocol (all 8 steps)
- [ ] Lists all cardinal rules (no creative edits post-approval, always use templates, always update cross-references, always update index)
- [ ] Explains cross-reference maintenance rules
- [ ] Explains the three-tier + sidecar architecture
- [ ] Plain text format (no YAML frontmatter)

### Templates

- [ ] `templates/location.template.md` exists
- [ ] `templates/faction.template.md` exists
- [ ] `templates/npc.template.md` exists
- [ ] `templates/event.template.md` exists
- [ ] `templates/culture.template.md` exists
- [ ] `templates/lexicon-entry.template.md` exists
- [ ] `templates/thread-entry.template.md` exists
- [ ] `templates/GUIDE.md` exists and is comprehensive

---

## 3. Schema Verification

Verify that all YAML frontmatter blocks are syntactically valid and contain required fields.

### Frontmatter Syntax

- [ ] All YAML frontmatter blocks parse correctly (test with an online YAML validator or `yaml.safe_load()`)
- [ ] All frontmatter blocks are properly delimited with `---` on opening and closing lines

### Required Fields — Tier 3 Templates

For each template (`location`, `faction`, `npc`, `event`, `culture`), verify:

- [ ] `type` field present (matches template type)
- [ ] `name` field present (empty string placeholder)
- [ ] `tier` field present (value: `3`)
- [ ] `references` field present (empty array `[]`)
- [ ] `last_updated` field present (placeholder date)

### Type-Specific Fields

- [ ] Location template has: `category` (planet|moon|station|settlement|region), `parent_body`, `status` (active|abandoned|contested|restricted), `controlled_by`
- [ ] Faction template has: `category` (corporation|clan|government|insurgency|religious|military|other), `allegiance`, `status` (active|dissolved|underground|rising|declining), `leader`, `base_of_operations`
- [ ] NPC template has: `category` (leader|diplomat|soldier|civilian|criminal|scholar|other), `faction`, `location`, `status` (alive|dead|missing|unknown), `disposition` (friendly|neutral|hostile|complicated)
- [ ] Event template has: `category` (battle|political|disaster|discovery|cultural|personal), `date`, `location`, `key_actors` (array), `status` (historical|ongoing|imminent|secret)
- [ ] Culture template has: `category` (ethnic|regional|religious|professional|other), `associated_faction`, `associated_location`

### Index Frontmatter

- [ ] Each index file has `type: index`
- [ ] Each index file has `category` field matching its content type
- [ ] Each index file has `entry_count` field (value: `0` for initial scaffold)
- [ ] Each index file has `last_updated` field

### Spine Frontmatter

- [ ] `spine/current-state.md` has `type: spine`
- [ ] Has `last_session` field (placeholder date)
- [ ] Has `last_updated` field

### Sidecar Frontmatter

- [ ] `sidecar/lexicon.md` has `type: lexicon`
- [ ] Has `entry_count` field (value: `0`)
- [ ] Has `last_updated` field
- [ ] `sidecar/threads.md` has `type: threads`
- [ ] Has `entry_count` field (value: `0`)
- [ ] Has `last_updated` field

---

## 4. Cross-Link Verification

Verify that all internal references and paths resolve correctly.

### Directory README References

- [ ] `spine/README.md` references correct relative paths (to root, to index, etc.)
- [ ] `index/README.md` references correct relative paths (to lore categories, etc.)
- [ ] `lore/README.md` references correct relative paths (to subdirectories, to templates)
- [ ] `sidecar/README.md` references correct relative paths (to lore, to index)
- [ ] `templates/README.md` references correct relative paths (to GUIDE.md, to lore)

### Root README References

- [ ] Root README references `spine/` directory correctly
- [ ] Root README references `index/` directory correctly
- [ ] Root README references `lore/` directory correctly
- [ ] Root README references `sidecar/` directory correctly
- [ ] Root README references `templates/` directory correctly
- [ ] Root README references `.clinerules` correctly
- [ ] Root README references `VERIFICATION.md` correctly

### Template Cross-Reference Format

- [ ] Template examples use the `type:slug` format for references (e.g., `faction:example-slug`)
- [ ] Reference examples in templates show the correct type prefix for their category

---

## 5. Content Verification

Verify that initial placeholder content is correct.

### Spine Content

- [ ] `spine/current-state.md` contains `## Current Mission` section
- [ ] Contains `## Player Character Status` section
- [ ] Contains `## Active NPCs` section
- [ ] Contains `## Unresolved Tensions` section
- [ ] Contains `## Recent Developments` section
- [ ] Contains `## Next Session Prep` section
- [ ] All sections contain `<!-- Not yet started -->` placeholder

### Sidecar Content

- [ ] `sidecar/lexicon.md` has an instructional example entry showing the format: `**[Term]** — [Definition]. *See: [type:slug]*`
- [ ] `sidecar/threads.md` has an instructional example entry showing the format: `**[Entity A]** → **[Entity B]** | [Relationship]: [Description]. *Relevant entries: [type:slug]*`

### Index Content

- [ ] `index/factions.md` has an empty table with correct headers: `| Name | Type/Category | Status | Key Detail | Lore Entry |`
- [ ] `index/locations.md` has an empty table with correct headers
- [ ] `index/npcs.md` has an empty table with correct headers
- [ ] `index/events.md` has an empty table with correct headers

### Template Content

- [ ] All templates have YAML frontmatter with placeholder values
- [ ] All templates have markdown section headers with HTML comment instructions
- [ ] All templates reference `templates/GUIDE.md` for comprehensive usage guidance
- [ ] Templates contain inline guidance on what content belongs in each section

---

## Verification Complete

- [ ] All items in sections 1-5 are checked
- [ ] Any issues found have been corrected and re-verified

**Date verified**: _______________  
**Verified by**: _______________

&nbsp;
