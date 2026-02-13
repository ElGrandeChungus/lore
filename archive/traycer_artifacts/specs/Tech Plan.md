## Architectural Approach

### Core architectural decisions

**1. Hybrid implementation strategy**

The scaffold will be created through a combination of manual key-file creation and scripted generation for repetitive structures:

- **Manual creation**: Root README, .clinerules, templates/README.md, and one complete example template (location.template.md) to establish the pattern
- **Script generation**: Remaining templates (faction, NPC, event, culture, lexicon-entry, thread-entry), all directory READMEs, empty index files, spine file, sidecar files
- **Rationale**: Manual creation ensures the most critical navigation documents are carefully crafted with full context. Script generation handles the mechanical repetition (5 more templates, 6+ directory READMEs) while maintaining consistency.

**2. Document-centric architecture (not software)**

This is a knowledge base, not an application. The "architecture" is the structure of documents and their relationships:

- **No runtime system**: No servers, APIs, or databases
- **No build process**: No compilation, bundling, or deployment
- **Git as the system of record**: Version control is the only "backend"
- **Markdown + YAML as the interface**: Documents are both human-readable and machine-parseable
- **Cline as the "runtime"**: The AI agent navigates and maintains the structure through conversational workflows

**3. Layered information architecture**

Documents are organized in a strict hierarchy that mirrors the three-tier + sidecar model:

```
Root (orientation layer)
├── Spine (Tier 1: current state)
├── Index (Tier 2: scannable reference)
├── Lore (Tier 3: deep canonical entries)
│   └── [category subdirectories]
├── Sidecar (cross-cutting concerns)
└── Templates (structural blueprints)
```

Each layer has a specific token budget and loading pattern:

- **Always loaded**: Root README, .clinerules, Spine, Index, Sidecar (~1500-2000 tokens total)
- **Loaded on demand**: Tier 3 entries (200-2000 tokens each)
- **Never loaded in bulk**: Templates (used for creation, not querying)

**4. Hybrid cross-reference system**

References between entries use **type-prefixed slugs** (`faction:crimson-fleet`, `location:seicoe-station`):

- **Explicit enough** to validate (type prefix enables category checking)
- **Flexible enough** to survive renames (slug can be updated without breaking all references)
- **Resolvable** via index lookup (index maps slugs to file paths)
- **Human-readable** in YAML frontmatter and staging diffs

**5. Schema-validated YAML frontmatter**

All entries (templates, lore files, index files, spine, sidecar) use YAML frontmatter with defined schemas:

- **Required fields** enforced per entry type (e.g., location requires `type`, `name`, `tier`, `category`)
- **Type checking** for field values (strings, arrays, enums)
- **No semantic validation** in initial scaffold (cross-reference integrity checked during encoding, not at rest)
- **Validation approach**: Manual checklist for initial scaffold; future encoding workflows re-validate on write

**6. Comprehensive + layered documentation**

READMEs follow a "quick-start + deep-dive" pattern:

- **Root README**: Layered structure with quick-start section (50 lines) + detailed architecture/protocol sections (200+ lines total)
- **Directory READMEs**: Comprehensive (100-150 lines each) with examples, edge cases, and decision rubrics
- **Template guidance**: Both inline HTML comments (quick reference) + separate templates/GUIDE.md (comprehensive usage manual)
- **Rationale**: First-time users get orientation quickly; Cline can reference deep details on demand without re-reading everything

**7. Manual verification with documented checklist**

Success criteria validation is manual, guided by a comprehensive checklist:

- **No verification script** (avoids script maintenance burden for a one-time scaffold)
- **Documented checklist** in root README or separate VERIFICATION.md
- **Checklist items**: Directory existence, README presence, frontmatter syntax, cross-link correctness, template completeness
- **Trade-off**: Slower initial validation, but simpler to understand and adjust

---

## Data Model

This section defines the document schemas (YAML frontmatter + markdown structure) for each entity type in the knowledge base.

### 1. Tier 3 Lore Entries

All canonical lore entries share a common frontmatter structure with type-specific extensions.

**Base schema (all lore entries)**:

```yaml
type: <entry-type>           # enum: location | faction | npc | event | culture
name: <string>               # canonical entity name
tier: 3                      # always 3 for lore entries
references: []               # array of type-prefixed slugs (e.g., ["faction:crimson-fleet"])
last_updated: <YYYY-MM-DD>   # ISO date string
```

**Location-specific extensions**:

```yaml
category: <string>           # enum: planet | moon | station | settlement | region
parent_body: <string>        # what it orbits or is part of (optional)
status: <string>             # enum: active | abandoned | contested | restricted
controlled_by: <string>      # faction slug or "disputed"
```

**Faction-specific extensions**:

```yaml
category: <string>           # enum: corporation | clan | government | insurgency | religious | military | other
allegiance: <string>         # primary political alignment
status: <string>             # enum: active | dissolved | underground | rising | declining
leader: <string>             # NPC slug (optional)
base_of_operations: <string> # location slug (optional)
```

**NPC-specific extensions**:

```yaml
category: <string>           # enum: leader | diplomat | soldier | civilian | criminal | scholar | other
faction: <string>            # faction slug (optional)
location: <string>           # location slug (current location)
status: <string>             # enum: alive | dead | missing | unknown
disposition: <string>        # enum: friendly | neutral | hostile | complicated
```

**Event-specific extensions**:

```yaml
category: <string>           # enum: battle | political | disaster | discovery | cultural | personal
date: <string>               # in-universe date or relative timing
location: <string>           # location slug where it happened
key_actors: []               # array of NPC/faction slugs
status: <string>             # enum: historical | ongoing | imminent | secret
```

**Culture-specific extensions**:

```yaml
category: <string>           # enum: ethnic | regional | religious | professional | other
associated_faction: <string> # faction slug (optional)
associated_location: <string># location slug (optional)
```

### 2. Index Files (Tier 2)

Index files are markdown tables with YAML frontmatter for metadata.

**Index frontmatter schema**:

```yaml
type: index
category: <string>           # enum: factions | locations | npcs | events
entry_count: <number>        # auto-updated count of rows
last_updated: <YYYY-MM-DD>
```

**Index table structure**:

```markdown
| Name | Type/Category | Status | Key Detail | Lore Entry |
|------|---------------|--------|------------|------------|
| [Name] | [subcategory] | [status] | [one key fact] | [type:slug or "—"] |
```

### 3. Spine (Tier 1)

Campaign state document with fixed section structure.

**Spine frontmatter schema**:

```yaml
type: spine
last_session: <YYYY-MM-DD>   # date of last play session
last_updated: <YYYY-MM-DD>
```

**Spine sections** (markdown headers):

- `## Current Mission`
- `## Player Character Status`
- `## Active NPCs`
- `## Unresolved Tensions`
- `## Recent Developments`
- `## Next Session Prep`

Initial state: Each section contains a placeholder comment: `<!-- Not yet started -->`

### 4. Sidecar Files

**Lexicon frontmatter schema**:

```yaml
type: lexicon
entry_count: <number>
last_updated: <YYYY-MM-DD>
```

**Lexicon entry format** (inline in lexicon.md):

```markdown
**[TERM]** — [Definition, 15-30 words max]. *See: [type:slug if applicable]*
```

**Example entry** (instructional):

```markdown
**[Example Term]** — [Brief definition explaining what this term means in-universe]. *See: [faction:example-slug]*
```

**Threads frontmatter schema**:

```yaml
type: threads
entry_count: <number>
last_updated: <YYYY-MM-DD>
```

**Thread entry format** (inline in threads.md):

```markdown
**[ENTITY A]** → **[ENTITY B]** | [Relationship type]: [Description, 1-2 sentences]. *Relevant entries: [type:slug, type:slug]*
```

**Example entry** (instructional):

```markdown
**[PC Name]** → **[Location/Faction]** | [Connection type]: [How this PC relates to this canonical element]. *Relevant entries: [location:example-slug]*
```

### 5. Templates

Templates are structural blueprints, not data. They have the same frontmatter schemas as their target entry types, but with placeholder values and instructional comments.

**Template naming convention**: `<type>.template.md` (e.g., `location.template.md`)

**Template content structure**:

- YAML frontmatter with empty/placeholder values
- Markdown sections with HTML comment instructions
- Inline guidance on what content belongs in each section

**Example (location template excerpt)**:

```yaml
---
type: location
name: ""
tier: 3
category: "" # planet | moon | station | settlement | region
# ... other fields
---

# [Location Name]

## Physical Description
<!-- Describe geography, atmosphere, climate, notable physical features.
     For planets: orbital characteristics, biosphere, habitability.
     For stations: size, configuration, docking capacity.
     Keep to 2-3 paragraphs. -->
```

### 6. Configuration Files

**.clinerules** (plain text, no frontmatter):

- Persistent instruction set for Cline
- Encoding protocol steps
- Cardinal rules (no creative edits post-approval, always use templates, etc.)
- Cross-reference maintenance rules

**.gitignore** (plain text):

- OS files: `.DS_Store`, `Thumbs.db`, `desktop.ini`
- Editor configs: `.vscode/`, `.idea/`, `*.swp`, `*~`, `.project`, `.settings/`
- Temporary files: `*.tmp`, `*.bak`, `~$*`

---

## Component Architecture

This section defines the structural components (directories, key files, and their relationships) and how they integrate to form the complete knowledge base.

### 1. Directory Structure (Component Hierarchy)

```
taito-system/                    [Root component]
├── .clinerules                  [Persistent agent instructions]
├── .gitignore                   [VCS ignore rules]
├── README.md                    [Root navigation guide]
├── VERIFICATION.md              [Manual verification checklist]
│
├── spine/                       [Tier 1 component]
│   ├── README.md               [Spine usage guide]
│   └── current-state.md        [Campaign state document]
│
├── index/                       [Tier 2 component]
│   ├── README.md               [Index purpose & format guide]
│   ├── factions.md             [Faction index table]
│   ├── locations.md            [Location index table]
│   ├── npcs.md                 [NPC index table]
│   └── events.md               [Event index table]
│
├── lore/                        [Tier 3 component]
│   ├── README.md               [Lore organization guide]
│   ├── locations/
│   │   ├── README.md           [Location entry guide]
│   │   └── .gitkeep            [Preserve empty directory]
│   ├── factions/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── npcs/
│   │   ├── README.md
│   │   └── .gitkeep
│   ├── events/
│   │   ├── README.md
│   │   └── .gitkeep
│   └── cultures/
│       ├── README.md
│       └── .gitkeep
│
├── sidecar/                     [Cross-cutting component]
│   ├── README.md               [Lexicon vs threads distinction]
│   ├── lexicon.md              [Universe vocabulary]
│   └── threads.md              [Campaign-to-lore connections]
│
└── templates/                   [Structural blueprints component]
    ├── README.md               [Template usage guide]
    ├── GUIDE.md                [Comprehensive template manual]
    ├── location.template.md
    ├── faction.template.md
    ├── npc.template.md
    ├── event.template.md
    ├── culture.template.md
    ├── lexicon-entry.template.md
    └── thread-entry.template.md
```

### 2. Component Responsibilities

**Root component** (`/`):

- **Orientation**: First point of contact for Cline and GM
- **Navigation**: Explains the architecture and how to traverse it
- **Rules**: Establishes encoding protocol and cardinal rules via .clinerules
- **Verification**: Provides manual checklist for scaffold validation

**Spine component** (`/spine/`):

- **Current state tracking**: Single source of truth for "where are we now"
- **Session continuity**: Updated after each game session
- **Lightweight**: Designed to always fit in context window (~300-500 tokens)
- **Volatile**: Changes frequently, resets between campaigns

**Index component** (`/index/`):

- **Entity inventory**: Scannable reference of everything that exists
- **Navigation aid**: Maps entity names to lore entry locations
- **Relationship preview**: One-line summaries of key relationships
- **Always loaded**: Part of baseline context for all queries

**Lore component** (`/lore/`):

- **Canonical truth**: Deep, authoritative entries for universe elements
- **Category organization**: Subdirectories by entity type for navigability
- **On-demand loading**: Entries loaded only when relevant to query
- **Reusable**: Campaign-agnostic content that survives campaign resets

**Sidecar component** (`/sidecar/`):

- **Lexicon**: Universe-specific vocabulary (campaign-agnostic)
- **Threads**: Campaign-specific narrative connections (volatile)
- **Always loaded**: Part of baseline context to prevent hallucinated terminology
- **Incubation**: Lexicon serves as staging area for concepts not yet worthy of full entries

**Templates component** (`/templates/`):

- **Structural blueprints**: Define schemas and section structures
- **Encoding guidance**: Inline comments + comprehensive guide
- **Never loaded for queries**: Used only during entry creation
- **Consistency enforcement**: Ensures all entries follow standard formats

### 3. Integration Points & Data Flow

**Query flow** (Cline navigates to answer a question):

```
1. Load: Root README → .clinerules (first-time orientation)
2. Load: Spine + Index + Sidecar (baseline context)
3. Parse: Index to identify relevant entities
4. Load: Specific Tier 3 entries based on query
5. Follow: Cross-references (type:slug) to related entries
6. Answer: With moderate citations (Entity (Category))
```

**Encoding flow** (GM commits new lore):

```
1. Trigger: GM uses encode phrase
2. Classify: Cline determines entry type(s)
3. Load: Appropriate template(s) from /templates/
4. Identify: Cross-references and index impacts
5. Re-read: Impacted documents (hybrid editing resilience)
6. Stage: Hybrid format (overview + new-file content + changed sections)
7. Approve: GM reviews and approves
8. Write: Cline commits to /lore/, /index/, /sidecar/ as needed
```

**Cross-reference resolution**:

```
Type-prefixed slug (e.g., "faction:crimson-fleet")
  ↓
Index lookup (factions.md)
  ↓
File path resolution (lore/factions/crimson-fleet.md)
  ↓
Load entry and follow further references
```

### 4. Failure Modes & Resilience

**Manual edits outside Cline**:

- **Risk**: Cross-references become stale, index out of sync
- **Mitigation**: Cline re-reads impacted documents before staging (Flow 1, Step 5)
- **Detection**: Cross-reference fixes flagged during next encoding operation

**Missing referenced entries**:

- **Risk**: Reference points to non-existent entry
- **Mitigation**: Index serves as source of truth; broken references flagged in staging
- **Recovery**: GM decides whether to create missing entry or remove reference

**YAML frontmatter syntax errors**:

- **Risk**: Malformed YAML breaks parsing
- **Mitigation**: Schema validation during manual verification checklist
- **Recovery**: Manual correction by GM (YAML is human-readable)

**Directory structure corruption**:

- **Risk**: Missing READMEs or directories
- **Mitigation**: Manual verification checklist checks directory structure
- **Recovery**: Regenerate missing components using templates/GUIDE.md

### 5. Verification Checklist (Manual)

The `VERIFICATION.md` file will contain a structured checklist covering:

**Structure verification**:

- [ ] All required directories exist (spine, index, lore/[5 categories], sidecar, templates)
- [ ] All directories have README.md files
- [ ] All .gitkeep files present in empty lore subdirectories

**Document verification**:

- [ ] Root README.md has quick-start + detailed sections
- [ ] .clinerules contains encoding protocol and cardinal rules
- [ ] All 7 templates exist in /templates/
- [ ] templates/GUIDE.md exists and is comprehensive

**Schema verification**:

- [ ] All YAML frontmatter blocks parse correctly (use online YAML validator)
- [ ] Required fields present in each template (type, name, tier, references, last_updated)
- [ ] Enum values match specifications (e.g., location category: planet|moon|station|settlement|region)

**Cross-link verification**:

- [ ] Directory READMEs reference correct relative paths
- [ ] Root README references correct directory paths
- [ ] Template examples use type:slug format for references

**Content verification**:

- [ ] Spine sections have "Not yet started" placeholders
- [ ] Sidecar files have instructional example entries
- [ ] Index files have empty tables with correct headers
- [ ] Templates have inline HTML comments + reference to GUIDE.md

&nbsp;