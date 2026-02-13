# Template Authoring Guide

This guide is the comprehensive reference for all templates in `templates/`.
Use it when creating new canonical entries or validating existing ones.

## 1. What Templates Are For

Templates are contract documents.
They define required metadata, required sections, and expected granularity.
They prevent schema drift and reduce ambiguity during future retrieval.

Use templates to ensure:

- Stable frontmatter keys for machine parsing.
- Comparable section structure across entries.
- Predictable cross-reference behavior.
- Cleaner staging diffs for GM review.

Do not use templates as query material.
They are creation tools, not world-state records.

## 2. Global Conventions

### 2.1 Frontmatter Rules

- Open and close frontmatter with `---`.
- Keep required fields present even when values are temporarily empty.
- Keep field names lowercase with underscores.
- Use quoted placeholders for string fields when empty.
- Use arrays for list fields, even if currently empty.

### 2.2 Cross-Reference Format

All references use type-prefixed slugs:

- `location:<slug>`
- `faction:<slug>`
- `npc:<slug>`
- `event:<slug>`
- `culture:<slug>`

Slug rules:

- Lowercase letters and numbers.
- Hyphen-separated words.
- No spaces, underscores, or punctuation.

Examples:

- `faction:crimson-fleet`
- `location:seicoe-station`
- `npc:commander-voss`
- `event:battle-of-mirren`
- `culture:daysail-nomads`

### 2.3 Writing Style

- Prefer specific factual claims over broad flavor prose.
- Keep paragraphs short and scannable.
- Use bullets for lists of assets, relationships, or timeline beats.
- Mark uncertainty explicitly in `Notes`, not core sections.
- Record only canon accepted by the GM.

### 2.4 Update Workflow

1. Choose template type.
2. Copy template into `lore/<category>/`.
3. Fill frontmatter.
4. Fill markdown sections.
5. Validate references.
6. Update index and sidecar as needed.
7. Re-read impacted files before staging.

## 3. Type Selection and Edge Cases

### 3.1 Quick Decision Matrix

- Place-centric content -> `location`
- Group/organization content -> `faction`
- Person-centric content -> `npc`
- Time-bounded incident -> `event`
- Shared customs/values identity -> `culture`

### 3.2 Ambiguous Cases

Case: mobile fleet city.
Guidance: classify as `location` if treated as a place where scenes occur; use `faction` for the operating authority.

Case: legendary founder myth.
Guidance: if it is an individual with actionable relevance, use `npc`; if mostly historical incident, use `event`.

Case: professional guild doctrine.
Guidance: if doctrine and shared practice are the focus, use `culture`; if command and operations are the focus, use `faction`.

Case: recurring military operation.
Guidance: use `event` for each notable operation; use `faction` for the organization running them.

### 3.3 Lexicon vs Full Entry

Use lexicon inline entry when:

- The concept is definitional.
- One sentence can capture it.
- No timeline, relationships, or stakes need detail.

Promote to full Tier 3 when:

- The concept drives decisions or conflict.
- Multiple entities interact around it.
- It needs dedicated history or consequences.

## 4. Location Template Guide

### 4.1 Required Frontmatter

```yaml
type: location
name: ""
tier: 3
category: ""        # planet | moon | station | settlement | region
parent_body: ""
status: ""          # active | abandoned | contested | restricted
controlled_by: ""   # faction:<slug> | disputed | none
references: []
last_updated: "YYYY-MM-DD"
```

### 4.2 Section Intent

- `Physical Description`: tangible environment and operational access.
- `Political Status`: control, enforcement, and contested claims.
- `Significance`: why this place matters strategically or symbolically.
- `Key Sites`: mission-relevant internal points of interest.
- `History`: concise chronology that explains current state.
- `Notes`: unresolved issues and maintenance tasks.

### 4.3 Good Entry Example (Short Form)

```markdown
## Key Sites
- **Drydock 9**: Primary heavy-frame maintenance berth and black-market retrofit node.
- **Sunline Bazaar**: Tax-free exchange corridor controlled by contractor syndicates.
```

## 5. Faction Template Guide

### 5.1 Required Frontmatter

```yaml
type: faction
name: ""
tier: 3
category: ""            # corporation | clan | government | insurgency | religious | military | other
allegiance: ""
status: ""              # active | dissolved | underground | rising | declining
leader: ""              # npc:<slug>
base_of_operations: ""  # location:<slug>
references: []
last_updated: "YYYY-MM-DD"
```

### 5.2 Section Intent

- `Overview`: identity and role at a glance.
- `Structure and Leadership`: authority model and practical power.
- `Goals and Motivations`: why the faction acts.
- `Resources and Capabilities`: what it can actually deploy.
- `Relationships`: allies, rivals, dependencies.
- `Cultural Identity`: internal ethos and external signaling.
- `History`: phases, shifts, and inflection points.
- `Notes`: unresolved canon/maintenance items.

### 5.3 Good Entry Example (Short Form)

```markdown
## Relationships
- **faction:harbor-compact**: patron - provides legal shielding in exchange for convoy protection.
- **faction:iron-reckoning**: rival - competes for salvage rights and sabotages tenders.
```

## 6. NPC Template Guide

### 6.1 Required Frontmatter

```yaml
type: npc
name: ""
tier: 3
category: ""      # leader | diplomat | soldier | civilian | criminal | scholar | other
faction: ""       # faction:<slug>
location: ""      # location:<slug>
status: ""        # alive | dead | missing | unknown
disposition: ""   # friendly | neutral | hostile | complicated
references: []
last_updated: "YYYY-MM-DD"
```

### 6.2 Section Intent

- `Appearance and First Impression`: immediate sensory read.
- `Role and Position`: formal role and real influence.
- `Personality and Motivation`: behavior drivers and contradictions.
- `Relationships`: ties with operational consequences.
- `Knowledge and Secrets`: information asymmetry and risk.
- `Combat Profile`: fiction-facing threat behavior.
- `Notes`: unresolved canon and upkeep tasks.

### 6.3 Good Entry Example (Short Form)

```markdown
## Knowledge and Secrets
- Knows the quiet jump windows used by smuggler escorts.
- Conceals an old command failure tied to event:skylane-collapse.
```

## 7. Event Template Guide

### 7.1 Required Frontmatter

```yaml
type: event
name: ""
tier: 3
category: ""      # battle | political | disaster | discovery | cultural | personal
date: ""
location: ""      # location:<slug>
key_actors: []    # npc:<slug> and/or faction:<slug>
status: ""        # historical | ongoing | imminent | secret
references: []
last_updated: "YYYY-MM-DD"
```

### 7.2 Section Intent

- `Summary`: single-paragraph account of the event.
- `Context`: conditions that produced the event.
- `Key Details`: concrete timeline and participant specifics.
- `Consequences`: immediate and long-tail effects.
- `Open Questions`: unresolved facts with campaign relevance.
- `Notes`: evidence confidence and follow-up tasks.

### 7.3 Good Entry Example (Short Form)

```markdown
## Consequences
- Transit insurance rates doubled across the inner route.
- faction:frontier-assembly lost local legitimacy after delayed relief.
```

## 8. Culture Template Guide

### 8.1 Required Frontmatter

```yaml
type: culture
name: ""
tier: 3
category: ""              # ethnic | regional | religious | professional | other
associated_faction: ""    # faction:<slug>
associated_location: ""   # location:<slug>
references: []
last_updated: "YYYY-MM-DD"
```

### 8.2 Section Intent

- `Overview`: who belongs and where the culture lives.
- `Values and Beliefs`: internal logic and taboos.
- `Language and Communication`: registers, signals, and codes.
- `Social Structure`: status, role distribution, mobility.
- `Aesthetic and Material Culture`: visible practices and artifacts.
- `Relationship to Power`: institutional alignment and friction.
- `Notes`: uncertain claims and maintenance actions.

### 8.3 Good Entry Example (Short Form)

```markdown
## Values and Beliefs
Members frame debt as stewardship, not obligation; default is mutual rescue, and refusing aid without cause is a severe status stain.
```

## 9. Lexicon Entry Pattern

Lexicon entries live inline in `sidecar/lexicon.md`.
They do not use frontmatter.

Required format:

`**[TERM]** - [Definition, 15-30 words max]. *See: [type:slug if applicable]*`

Good example:

`**Dock Silence** - Temporary radio blackout protocol used during customs sweeps to hide smuggler reroutes. *See: [location:seicoe-station]*`

When to use:

- Terminology clarification.
- Brief concept labels.
- Abbreviations and slogans.

When not to use:

- Concepts requiring timeline and conflict detail.
- Entities that need dedicated canonical sections.

## 10. Thread Entry Pattern

Thread entries live inline in `sidecar/threads.md`.
They do not use frontmatter.

Required format:

`**[ENTITY A]** -> **[ENTITY B]** | [Relationship type]: [Description, 1-2 sentences]. *Relevant entries: [type:slug, type:slug]*`

Good example:

`**PC: Idris Vale** -> **Harbor Compact** | Debt leverage: Compact legal shields Idris's crew in exchange for covert transport jobs. *Relevant entries: [npc:idris-vale, faction:harbor-compact]*`

Usage rules:

- Keep threads campaign-specific and update frequently.
- Keep canonical details in `lore/`; keep moment-to-moment tensions in `threads.md`.
- Remove or revise stale threads after major sessions.

## 11. Quality Checklist Before Staging

- Frontmatter parses as valid YAML.
- Required keys are present and spelled correctly.
- Enum values are from approved sets.
- Cross-reference slugs are type-prefixed and plausible.
- Section headers match template exactly.
- Notes section does not contain unresolved canon disguised as fact.
- Related index updates are prepared.
- Sidecar additions are prepared when needed.

## 12. Common Failure Modes

Failure: mixing entity types in one file.
Fix: split primary entity into correct type and use references for connections.

Failure: overfilling notes with essential canon.
Fix: move stable facts into primary sections; keep notes operational.

Failure: dangling references.
Fix: check index files, create missing entries, or remove invalid slugs.

Failure: writing long prose without structure.
Fix: use concise paragraphs plus bullets for discrete facts.

Failure: skipping consequences for events.
Fix: add immediate and long-term impact statements.

Failure: using lexicon for major institutions.
Fix: promote to faction/location/culture entry.

## 13. Recommended Validation Commands

Use these from repository root:

```powershell
rg --files templates
```

```powershell
Get-Content -Raw templates/location.template.md
```

```powershell
@'
import yaml, pathlib
for p in [
    "templates/location.template.md",
    "templates/faction.template.md",
    "templates/npc.template.md",
    "templates/event.template.md",
    "templates/culture.template.md",
]:
    text = pathlib.Path(p).read_text(encoding="utf-8")
    fm = text.split("---", 2)[1]
    yaml.safe_load(fm)
print("frontmatter ok")
'@ | python -
```

## 14. Final Notes

Start simple and accurate.
Prefer complete, cross-referenced entries over stylistic flourish.
Consistency is the quality multiplier for long-running campaign memory systems.
