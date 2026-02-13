## Summary

This Epic creates a git-tracked worldbuilding knowledge base for a Lancer RPG campaign that an AI agent (Cline) can navigate and maintain through conversation. It addresses the core limitation that no AI context window can hold an entire sci‑fi setting with hundreds of interlinked elements (locations, factions, NPCs, events, cultures, vocabulary, and live campaign state). The knowledge base must let the GM retrieve precise context quickly, preserve relationships between entities, and avoid hallucinated details by grounding answers in canon. The system is not a software application—its “interaction surface” is the repository’s structured documents and the encode/query workflows you run with Cline.

## Context & Problem

### Who’s affected

- **GM (primary):** needs fast, reliable recall and consistent continuity across sessions without manually curating a monolithic lorebook.
- **Cline (secondary):** needs a predictable navigation hierarchy and metadata to load only what’s necessary, reliably.
- **Players (indirect):** benefit from continuity, callbacks, and reduced retcons.

### Current pain

- **Token limits:** the full setting can’t be loaded at once; missing context causes wrong or incomplete answers.
- **Flat lorebooks:** either overload context or lose cross-links between related elements.
- **No encoding protocol:** brainstormed canon doesn’t reliably become structured, cross-referenced records.
- **Mixed concerns:** campaign-specific connections blur into reusable canon, making reuse and resets difficult.

## Assumptions / scope notes

- **Single-campaign-per-repo:** one campaign state (“Spine”) and one campaign-specific connections file (“Threads”); reuse happens by cloning/copying.
- **Hybrid editing:** the GM may edit files manually; Cline must assume the repository can change outside its control.

## Success criteria (initial scaffold)

- All required directories and documents exist.
- All templates and documents match the specified formats (including YAML frontmatter where required).
- Verification checks pass: every directory has a README, cross-links are correct, and frontmatter is syntactically valid.

&nbsp;