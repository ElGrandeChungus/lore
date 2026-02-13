# Taito System — Lancer Worldbuilding Memory System

> A git-tracked knowledge base that lets an AI agent (Cline) navigate, query, and maintain a sprawling sci-fi campaign world through conversation.

---

## Quick Start

### What is this?

This repository is the **system of record** for a Lancer RPG campaign setting. It solves the problem of AI context-window limits by organizing lore into a strict hierarchy that lets Cline load only what it needs, when it needs it.

### Three-Tier + Sidecar Architecture (at a glance)

| Tier | Directory    | Purpose                               | Load Behavior     |
|------|-------------|---------------------------------------|-------------------|
| 1    | `spine/`    | Current campaign state                | **Always loaded** |
| 2    | `index/`    | Scannable entity inventory (tables)   | **Always loaded** |
| 3    | `lore/`     | Deep canonical entries (by category)  | **On demand**     |
| —    | `sidecar/`  | Lexicon + campaign threads            | **Always loaded** |

**Templates** (`templates/`) provide structural blueprints for creating new entries. They are never loaded during queries.

### How to navigate

1. **Start here** — this README orients you to the structure and protocols.
2. **Read `.clinerules`** — persistent instructions Cline follows every session.
3. **Load baseline context** — `spine/current-state.md` + all `index/*.md` + both `sidecar/*.md`.
4. **Drill into `lore/`** — only when a query requires specific entity detail.
5. **Each directory has its own README** — read it before working in that directory.

### Key commands (for the GM)

- **Encode new lore**: Use an encode trigger phrase to start the encoding workflow.
- **Query lore**: Ask any lore question; Cline loads baseline context and drills down.
- **Post-session update**: Request a post-session update after a game session.
- **Promote a lexicon term**: Ask Cline to promote a term to a full entry.

---

## Architecture — Detailed

### Design Principles

This is a **document-centric knowledge base**, not a software application:

- **No runtime system** — no servers, APIs, or databases.
- **Git as the system of record** — version control is the only backend.
- **Markdown + YAML as the interface** — human-readable and machine-parseable.
- **Cline as the "runtime"** — the AI agent navigates and maintains the structure through conversational workflows.

### Information Hierarchy

```
taito-system/                    [Root — orientation layer]
├── .clinerules                  [Persistent agent instructions]
├── .gitignore                   [VCS ignore rules]
├── README.md                    [This file — root navigation guide]
├── VERIFICATION.md              [Manual verification checklist]
│
├── spine/                       [Tier 1 — current campaign state]
│   ├── README.md               [Spine usage guide]
│   └── current-state.md        [Campaign state document]
│
├── index/                       [Tier 2 — scannable entity tables]
│   ├── README.md               [Index purpose & format guide]
│   ├── factions.md             [Faction index table]
│   ├── locations.md            [Location index table]
│   ├── npcs.md                 [NPC index table]
│   └── events.md               [Event index table]
│
├── lore/                        [Tier 3 — deep canonical entries]
│   ├── README.md               [Lore organization guide]
│   ├── locations/
│   │   ├── README.md           [Location entry guide]
│   │   └── .gitkeep
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
├── sidecar/                     [Cross-cutting — vocabulary & connections]
│   ├── README.md               [Lexicon vs threads distinction]
│   ├── lexicon.md              [Universe vocabulary]
│   └── threads.md              [Campaign-to-lore connections]
│
└── templates/                   [Structural blueprints — encoding only]
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

### Token Budget Strategy

The system is designed with strict token budgets to fit within AI context windows:

| Component                  | Estimated Tokens | Load Frequency   |
|----------------------------|-----------------|------------------|
| Root README + .clinerules  | ~500-700        | First session    |
| Spine (current-state.md)   | ~300-500        | Every query      |
| Index (all 4 files)        | ~400-600        | Every query      |
| Sidecar (lexicon + threads)| ~300-500        | Every query      |
| **Baseline total**         | **~1500-2000**  | **Every query**  |
| Single Tier 3 entry        | ~200-2000       | On demand        |

### Loading Pattern

For any lore interaction, Cline follows this loading priority:

1. **First-time only**: Root README → `.clinerules` (full orientation)
2. **Always**: Spine + all Index files + both Sidecar files (baseline context)
3. **On demand**: Specific Tier 3 entries from `lore/` based on query needs
4. **For encoding only**: Appropriate template(s) from `templates/`

### Cross-Reference System

References between entities use **type-prefixed slugs**:

```
faction:crimson-fleet
location:seicoe-station
npc:commander-voss
event:battle-of-mirren
culture:daysail-nomads
```

- **Type prefix** enables category validation
- **Slugs** are lowercase, hyphen-separated
- **Index lookup** resolves slugs to file paths: `faction:crimson-fleet` → `lore/factions/crimson-fleet.md`
- **Used in**: YAML frontmatter `references` arrays, sidecar entries, and inline citations

---

## Encoding Protocol

The encoding protocol is the step-by-step workflow for turning new lore into structured, cross-referenced records. See `.clinerules` for the full protocol that Cline follows.

### Summary of Steps

1. **Summarize** — Cline summarizes what it believes became canon; GM confirms or corrects.
2. **Classify** — Cline determines entry type(s); proposes primary + secondary framing for ambiguous items.
3. **Decide depth** — If something could be a Lexicon term vs. a full entry, Cline asks.
4. **Identify impacts** — New entries, modified entries, index rows, cross-reference fixes.
5. **Repo-resilience check** — Re-read impacted documents before staging (hybrid editing support).
6. **Hybrid staging** — Present overview + new-file full content + modified-file changed sections.
7. **GM approval** — GM approves or requests adjustments.
8. **Commit** — Cline commits exactly what was staged, nothing more, nothing less.

---

## Cardinal Rules

These rules are inviolable and apply to every interaction:

1. **No creative edits post-approval** — Once the GM approves staging, Cline commits exactly what was staged. No additions, no rewording, no "improvements."
2. **Always use templates** — Every new Tier 3 entry must be created from the appropriate template in `templates/`.
3. **Always update cross-references** — When creating or modifying an entry, all references it touches must be checked and updated.
4. **Always update the index** — Every Tier 3 entry must have a corresponding row in the appropriate index file.

---

## Hybrid Editing Support

The GM may edit files manually outside of Cline. This means:

- **Cline must assume the repo can change** between interactions.
- **Before staging any changes**, Cline re-reads all impacted documents (encoding protocol step 5).
- **Cross-reference inconsistencies** introduced by manual edits are flagged and proposed as fixes during the next encoding operation.

---

## Related Documents

| Document             | Location                    | Purpose                                    |
|---------------------|-----------------------------|--------------------------------------------|
| Agent instructions  | `.clinerules`               | Persistent rules Cline reads every session |
| Verification        | `VERIFICATION.md`           | Manual scaffold validation checklist       |
| Spine guide         | `spine/README.md`           | How to use campaign state tracking         |
| Index guide         | `index/README.md`           | How index files work                       |
| Lore guide          | `lore/README.md`            | Lore organization and category rules       |
| Sidecar guide       | `sidecar/README.md`         | Lexicon vs. threads distinction            |
| Template guide      | `templates/README.md`       | Quick template usage reference             |
| Template manual     | `templates/GUIDE.md`        | Comprehensive template usage manual        |

---

## Version History

| Date       | Change                           | Author |
|------------|----------------------------------|--------|
| 2026-02-13 | Initial scaffold creation        | GM     |

&nbsp;
