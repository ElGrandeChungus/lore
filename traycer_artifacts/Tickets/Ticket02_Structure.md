## Scope

Create the complete directory structure and all template files that define the knowledge base architecture.

**Included**:

- All directories: spine/, index/, lore/, lore/locations/, lore/factions/, lore/npcs/, lore/events/, lore/cultures/, sidecar/, templates/
- All `.gitkeep` files in empty lore subdirectories
- templates/README.md (template usage guide)
- templates/GUIDE.md (comprehensive template manual)
- All 7 template files:
  - templates/location.template.md (manually created as the pattern example)
  - templates/faction.template.md
  - templates/npc.template.md
  - templates/event.template.md
  - templates/culture.template.md
  - templates/lexicon-entry.template.md
  - templates/thread-entry.template.md

**Explicitly out of scope**:

- Directory READMEs (handled in next ticket)
- Content files: spine, index, sidecar (handled in next ticket)

## Spec References

- **Tech Plan** (spec:b51fa6e9-64d7-49ca-8808-33201ddd3316/001e0d78-8198-4938-843b-a982a2191466):
  - Architectural Approach § 1 (Hybrid implementation: manual location.template.md, script for others)
  - Data Model § 1 (Tier 3 Lore Entries - all 5 type-specific schemas)
  - Data Model § 4 (Sidecar Files - lexicon and thread entry formats)
  - Data Model § 5 (Templates - structure and content)
  - Component Architecture § 1 (Directory Structure)

## Acceptance Criteria

### Directory Structure

- [ ] All 9 directories exist: spine, index, lore, lore/locations, lore/factions, lore/npcs, lore/events, lore/cultures, sidecar, templates
- [ ] All 5 lore subdirectories contain `.gitkeep` files
- [ ] Directory names match Tech Plan exactly (lowercase, no special characters)

### templates/README.md

- [ ] Explains template purpose and usage
- [ ] Lists all 7 templates with brief descriptions
- [ ] Explains the classification rubric (when to use which template)
- [ ] References templates/GUIDE.md for comprehensive guidance
- [ ] 50-100 lines

### templates/GUIDE.md

- [ ] Comprehensive manual for using all templates
- [ ] Explains YAML frontmatter schemas for each type
- [ ] Provides examples of well-formed entries
- [ ] Covers edge cases (ambiguous classification, lexicon vs full entry)
- [ ] Explains type-prefixed slug cross-reference format
- [ ] 200-300 lines

### location.template.md (Manual Creation - Pattern Example)

- [ ] Valid YAML frontmatter with all required fields from Tech Plan Data Model § 1
- [ ] Frontmatter includes: type, name, tier, category, parent_body, status, controlled_by, references, last_updated
- [ ] All enum values documented in comments (e.g., `category: "" # planet | moon | station | settlement | region`)
- [ ] Markdown sections: Physical Description, Political Status, Significance, Key Sites, History, Notes
- [ ] Each section has inline HTML comment with detailed instructional guidance
- [ ] Comments explain what content belongs, give examples, specify length guidelines

### faction.template.md

- [ ] Valid YAML frontmatter with faction-specific schema (Tech Plan Data Model § 1)
- [ ] Frontmatter includes: type, name, tier, category, allegiance, status, leader, base_of_operations, references, last_updated
- [ ] Markdown sections: Overview, Structure & Leadership, Goals & Motivations, Resources & Capabilities, Relationships, Cultural Identity, History, Notes
- [ ] Inline HTML comments with instructional guidance

### npc.template.md

- [ ] Valid YAML frontmatter with NPC-specific schema
- [ ] Frontmatter includes: type, name, tier, category, faction, location, status, disposition, references, last_updated
- [ ] Markdown sections: Appearance & First Impression, Role & Position, Personality & Motivation, Relationships, Knowledge & Secrets, Combat Profile, Notes
- [ ] Inline HTML comments with instructional guidance

### event.template.md

- [ ] Valid YAML frontmatter with event-specific schema
- [ ] Frontmatter includes: type, name, tier, category, date, location, key_actors, status, references, last_updated
- [ ] Markdown sections: Summary, Context, Key Details, Consequences, Open Questions, Notes
- [ ] Inline HTML comments with instructional guidance

### culture.template.md

- [ ] Valid YAML frontmatter with culture-specific schema
- [ ] Frontmatter includes: type, name, tier, category, associated_faction, associated_location, references, last_updated
- [ ] Markdown sections: Overview, Values & Beliefs, Language & Communication, Social Structure, Aesthetic & Material Culture, Relationship to Power, Notes
- [ ] Inline HTML comments with instructional guidance

### lexicon-entry.template.md

- [ ] Explains the inline format (not a standalone file template)
- [ ] Shows the format: `**[TERM]** — [Definition, 15-30 words max]. *See: [type:slug if applicable]*`
- [ ] Includes instructional example entry with bracketed placeholders
- [ ] Explains when to use lexicon vs full entry

### thread-entry.template.md

- [ ] Explains the inline format (not a standalone file template)
- [ ] Shows the format: `**[ENTITY A]** → **[ENTITY B]** | [Relationship type]: [Description]. *Relevant entries: [type:slug, type:slug]*`
- [ ] Includes instructional example entry with bracketed placeholders
- [ ] Explains the distinction between threads (campaign-specific) and canonical lore

## Dependencies

- **Requires**: `ticket:b51fa6e9-64d7-49ca-8808-33201ddd3316/[Foundation ticket ID]` (needs root README for context references)

## Implementation Notes

- `location.template.md` should be created manually first to establish the pattern; other templates can follow the same structure
- All YAML frontmatter must be syntactically valid (test with YAML parser)
- Inline HTML comments should be detailed enough to guide Cline during encoding without needing to reference GUIDE.md every time
- templates/GUIDE.md is the comprehensive reference; templates/README.md is the quick orientation

&nbsp;