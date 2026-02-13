## Scope

Create all directory READMEs and initial content files (spine, index, sidecar) to complete the scaffold.

**Included**:

- Directory READMEs (comprehensive, 100-150 lines each):
  - spine/README.md
  - index/README.md
  - lore/README.md
  - lore/locations/README.md
  - lore/factions/README.md
  - lore/npcs/README.md
  - lore/events/README.md
  - lore/cultures/README.md
  - sidecar/README.md
- Content files:
  - spine/current-state.md (with "Not yet started" placeholders)
  - index/factions.md (empty table with headers)
  - index/locations.md (empty table with headers)
  - index/npcs.md (empty table with headers)
  - index/events.md (empty table with headers)
  - sidecar/lexicon.md (with instructional example entry)
  - sidecar/threads.md (with instructional example entry)

**Explicitly out of scope**:

- Actual lore entries (those are created through the encoding workflow after scaffold is complete)

## Spec References

- **Tech Plan** (spec:b51fa6e9-64d7-49ca-8808-33201ddd3316/001e0d78-8198-4938-843b-a982a2191466):
  - Architectural Approach § 6 (Comprehensive + layered documentation for READMEs)
  - Data Model § 2 (Index Files)
  - Data Model § 3 (Spine)
  - Data Model § 4 (Sidecar Files)
  - Component Architecture § 2 (Component Responsibilities - explains what each README should cover)

## Acceptance Criteria

### Directory READMEs (All)

Each README must include these 5 sections (per Tech Plan):

- [ ] **Purpose**: What this directory contains (one paragraph)
- [ ] **Contents**: What files are here and what they cover
- [ ] **Format**: What template/format entries in this directory follow
- [ ] **Cross-references**: How entries here relate to entries in other directories
- [ ] **Update protocol**: When and how to update entries in this directory

### spine/README.md

- [ ] Explains Tier 1 purpose: current campaign state tracking
- [ ] Lists the 6 spine sections and what goes in each
- [ ] Explains post-session update workflow (Flow 3 from Core Flows)
- [ ] Notes that spine is volatile (resets between campaigns)
- [ ] References current-state.md structure
- [ ] 100-150 lines

### index/README.md

- [ ] Explains Tier 2 purpose: scannable entity inventory
- [ ] Describes the 4 index files and their table structures
- [ ] Explains how index maps entity names to lore entries (type:slug format)
- [ ] Notes that index is always loaded (part of baseline context)
- [ ] Explains when/how to update index (during encoding)
- [ ] 100-150 lines

### lore/README.md

- [ ] Explains Tier 3 purpose: deep canonical entries
- [ ] Lists the 5 category subdirectories
- [ ] Explains on-demand loading pattern
- [ ] References templates for entry creation
- [ ] Explains that lore is campaign-agnostic (reusable)
- [ ] 100-150 lines

### lore/[category]/README.md (5 files: locations, factions, npcs, events, cultures)

- [ ] Explains what entries belong in this category
- [ ] References the appropriate template
- [ ] Provides examples of well-formed entries
- [ ] Covers edge cases for classification
- [ ] Lists common cross-reference patterns for this category
- [ ] 100-150 lines each

### sidecar/README.md

- [ ] Explains the distinction between Lexicon (campaign-agnostic vocabulary) and Threads (campaign-specific connections)
- [ ] Describes when to use lexicon vs full entry
- [ ] Explains thread format and purpose
- [ ] Notes that sidecar is always loaded
- [ ] References lexicon-entry.template.md and thread-entry.template.md
- [ ] 100-150 lines

### spine/current-state.md

- [ ] Valid YAML frontmatter: `type: spine`, `last_session: ""`, `last_updated: ""`
- [ ] All 6 markdown sections present: Current Mission, Player Character Status, Active NPCs, Unresolved Tensions, Recent Developments, Next Session Prep
- [ ] Each section contains placeholder: `<!-- Not yet started -->`
- [ ] Well-formatted markdown

### index/[category].md (4 files: factions, locations, npcs, events)

- [ ] Valid YAML frontmatter: `type: index`, `category: [category]`, `entry_count: 0`, `last_updated: ""`
- [ ] Empty markdown table with correct headers: `| Name | Type/Category | Status | Key Detail | Lore Entry |`
- [ ] Table separator row present: `|------|---------------|--------|------------|------------|`
- [ ] No data rows (empty table ready for entries)

### sidecar/lexicon.md

- [ ] Valid YAML frontmatter: `type: lexicon`, `entry_count: 1`, `last_updated: ""`
- [ ] Contains one instructional example entry with bracketed placeholders
- [ ] Example follows format: `**[Example Term]** — [Brief definition explaining what this term means in-universe]. *See: [faction:example-slug]*`
- [ ] Includes a comment explaining this is an example to be replaced

### sidecar/threads.md

- [ ] Valid YAML frontmatter: `type: threads`, `entry_count: 1`, `last_updated: ""`
- [ ] Contains one instructional example entry with bracketed placeholders
- [ ] Example follows format: `**[PC Name]** → **[Location/Faction]** | [Connection type]: [How this PC relates to this canonical element]. *Relevant entries: [location:example-slug]*`
- [ ] Includes a comment explaining this is an example to be replaced

## Dependencies

- **Requires**: `ticket:b51fa6e9-64d7-49ca-8808-33201ddd3316/[Structure ticket ID]` (needs directory structure and templates to reference)

## Implementation Notes

- Directory READMEs are comprehensive (100-150 lines) with examples and edge cases—they're the primary reference for Cline when working in each area
- All content files should have valid YAML frontmatter that parses correctly
- Spine placeholders use HTML comments so they're invisible when rendered but clear when editing
- Sidecar example entries use bracketed placeholders to make it obvious they're instructional, not real lore
- Index tables are empty but properly formatted, ready to receive entries during encoding

&nbsp;