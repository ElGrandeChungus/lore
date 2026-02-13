# Sidecar Directory Guide

## Purpose

`sidecar/` stores cross-cutting context loaded for every query.
It complements Spine and Index by preserving vocabulary and active campaign links.
Sidecar is always loaded as part of baseline context.
This directory has two different functions:

- `lexicon.md` for campaign-agnostic terminology.
- `threads.md` for campaign-specific relationship state.

Use sidecar to reduce ambiguity in language and maintain narrative continuity.
Keep sidecar concise, current, and explicitly linked to canonical entries.
Do not use sidecar as a replacement for full Tier 3 lore files.

## Contents

Expected files in this directory:

- `sidecar/README.md`: operational guide for sidecar usage.
- `sidecar/lexicon.md`: vocabulary list with optional canonical pointers.
- `sidecar/threads.md`: active relationship graph for current campaign.

Template references:

- `templates/lexicon-entry.template.md`
- `templates/thread-entry.template.md`

Lexicon entry pattern:

`**[TERM]** — [Definition, 15-30 words max]. *See: [type:slug if applicable]*`

Thread entry pattern:

`**[ENTITY A]** → **[ENTITY B]** | [Relationship type]: [Description, 1-2 sentences]. *Relevant entries: [type:slug, type:slug]*`

Both files include YAML frontmatter metadata.
Both files are part of baseline query context.

## Format

`sidecar/lexicon.md` frontmatter:

- `type: lexicon`
- `entry_count: <number>`
- `last_updated: ""`

`sidecar/threads.md` frontmatter:

- `type: threads`
- `entry_count: <number>`
- `last_updated: ""`

Lexicon formatting rules:

- One line per term entry.
- Keep definition compact and unambiguous.
- Add `See:` slug only when it materially helps.

Thread formatting rules:

- One line per relationship thread.
- Keep statement present-tense and actionable.
- Include relevant canonical slugs whenever possible.

Do not place long prose paragraphs in sidecar files.
Do not duplicate large lore content from `lore/`.

## Cross-references

Lexicon cross-reference behavior:

- Terms may point to canonical entities in `lore/`.
- Useful when jargon maps to faction doctrine or location-specific concepts.

Thread cross-reference behavior:

- Threads should map campaign tensions to canonical entities.
- Typical targets: `npc`, `faction`, `location`, `event`.

Common integration patterns:

- Spine mentions active tension -> thread entry tracks relationship state.
- Thread references entity -> entity exists in index/lore.
- Lexicon introduces term -> optional `See:` points to canonical context.

Validation patterns:

- Every slug in sidecar resolves via index/lore.
- Threads reflect current campaign state; stale items are pruned.
- Lexicon avoids terms that require full entry depth.

## Update protocol

Update sidecar during encoding and post-session maintenance.
Recommended sequence:

1. Re-read `lexicon.md` and/or `threads.md` before editing.
2. Add, revise, or remove inline entries.
3. Recalculate `entry_count`.
4. Update `last_updated`.
5. Validate referenced slugs.
6. Stage with related lore/index updates.

Lexicon vs full entry decision:

- Use lexicon for short definitional terms.
- Promote to full lore entry when timeline, stakeholders, or structural impact appears.

Threads maintenance rules:

- Keep threads campaign-specific and volatile.
- Update after major sessions.
- Remove resolved threads that no longer influence play.
- Preserve unresolved threads that still drive future scenes.

Quality checks before commit:

- Frontmatter parses.
- Entry counts match actual lines.
- Formats match template patterns.
- Slugs resolve and are category-correct.

## Practical checklist

Run this pass after sidecar edits:

- Confirm file type (`lexicon` or `threads`) is correct.
- Recount entries and update `entry_count`.
- Update `last_updated`.
- Keep one entry per line.
- Keep lexicon definitions short and precise.
- Keep threads active and present-tense.
- Remove stale resolved threads.
- Ensure all slugs resolve through index/lore.
- Ensure new terms do not need full lore promotion.
- Ensure promoted terms were reflected in lexicon lines.
- Ensure thread lines map to actual campaign pressure.
- Ensure no long prose blocks were added.
- Re-read both files for consistency.
- Stage with related spine/lore/index changes.
- Submit staged changes for approval.
- Commit exactly approved content.
Common failure signals:

- `entry_count` does not match entry lines.
- Duplicate thread lines with conflicting states.
- Lexicon term has no clear definition.
- Thread uses entities not in index.
- Sidecar contains canonical detail better suited for `lore/`.

Related paths:

- `../README.md`
- `../lore/`
- `../index/`
- `../spine/current-state.md`
- `../templates/lexicon-entry.template.md`
- `../templates/thread-entry.template.md`
