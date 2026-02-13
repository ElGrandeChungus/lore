## Overview

This document defines the core user flows for the Lancer Worldbuilding Memory System. The primary interaction is conversational between the GM (you) and Cline (AI agent), with the repository acting as the system of record.

### Global conventions

- **Query baseline:** for any lore question, Cline starts by loading **Spine + Index + Sidecar**.
- **Citations:** answers cite **entity name + category** (e.g., “Seicoe Station (Location)…”).
- **Hybrid editing:** the GM may manually edit documents; Cline assumes the repo can change outside its control and re-checks anything it’s about to modify.
- **Staging standard (Hybrid):** staging is organized by change type, includes **full content for NEW files**, and **changed sections only** for modified files.

---

## Flow 1: Encode new lore

**Trigger / entry point:** GM uses an encode trigger phrase.

**Steps**:

1. Cline summarizes what it believes became canon; GM confirms/corrects.
2. Cline classifies each new fact; for ambiguous types, it proposes a primary + secondary framing (with reasoning).
3. If something could be Lexicon vs full entry, Cline asks which to do.
4. Cline identifies impacts: new entries, modified entries, index rows, cross-reference fixes.
5. **Repo-resilience check:** before staging, Cline re-reads any impacted documents (in case of manual edits).
6. Cline presents **Hybrid staging** (overview + new-file full content + modified-file changed sections).
7. GM approves or requests adjustments.
8. Cline commits exactly what was staged.

```mermaid
sequenceDiagram
  participant GM
  participant Cline
  participant Repo as Knowledge Base
  GM->>Cline: "encode this"
  Cline->>GM: Summarize canon; confirm?
  GM->>Cline: Confirm/correct
  Cline->>Cline: Classify + identify impacts
  Cline->>Repo: Re-read impacted docs
  Cline->>GM: Hybrid staging proposal
  GM->>Cline: Approve / adjust
  Cline->>Repo: Commit exactly staged
```

---

## Flow 2: Query lore (navigate + answer)

**Trigger / entry point:** GM asks a lore question.

**Steps**:

1. Cline loads Spine + Index + Sidecar to establish campaign context, entity inventory, vocabulary, and campaign-specific links.
2. Cline identifies which entities/entries are relevant and loads only what’s needed.
3. If the asked-about entity is **missing**, Cline asks clarifying questions to determine whether it is:
  - an existing element that isn’t recorded yet,
  - a new element being invented now, or
  - a session-only detail that should not become canon.
4. Cline answers conversationally and includes **moderate citations** (“Entity (Category) entry…”).

---

## Flow 3: Post-session update (Spine + implied canon)

**Trigger / entry point:** GM explicitly requests a post-session update.

**Steps**:

1. Cline asks what changed (mission, PCs, on-stage NPCs, tensions, developments, next prep).
2. Cline drafts an updated campaign state.
3. **Bundle by default:** if the session implies canon/index changes (e.g., NPC status, new faction), Cline includes them in the same staged set, with the GM free to decline any subset.
4. Cline presents Hybrid staging; GM approves/adjusts; Cline commits exactly staged.

---

## Flow 4: Cross-reference & consistency fixes (flag-and-propose)

**Trigger / entry point:** Cline detects inconsistency during any staging (encode, update, promotion).

**Steps**:

1. Cline identifies issues (one-way references, missing entries, stale index rows, conflicting metadata).
2. Cline includes a **Cross-Reference Fixes** section in staging with proposed corrections.
3. GM approves/declines fixes as part of the same staging decision.
4. Approved fixes are applied exactly as staged.

---

## Flow 5: Promote a Lexicon term to a full entry

**Trigger / entry point:** GM requests promotion of a term.

**Steps**:

1. Cline locates the term and asks what category it should become (location/faction/NPC/event/culture/etc.).
2. Cline stages: a new canonical entry + index row + an updated lexicon line that points to the new entry.
3. GM approves; Cline commits exactly staged.

---

## Flow 6: First-use orientation

**Trigger / entry point:** First time Cline opens the repository or receives a lore request.

**Steps**:

1. Cline reads the top-level navigation guide and the persistent rule set.
2. For any area it’s about to work in, Cline reads that area’s README first.
3. Cline loads Spine + Index + Sidecar and proceeds with query/encode flows.

&nbsp;