---
name: aido-map
description: Token-saving repo context workflow for OpenCode. Use this skill whenever user asks coding, debugging, refactor, feature work, or repo understanding that may involve multiple files. Always use this skill for repo-level tasks, architecture questions, endpoint changes, auth fixes, config edits, database work, UI updates, or test-impacting changes, even when user does not explicitly mention context maps.
compatibility:
  tools: Read, Glob, Grep, Edit, Write
---

# aido-map

Goal: reduce token usage by reading indexed repo context first, then reading only relevant source files.

## Core idea

Read `.aido` context before deep code exploration.
Do minimal reads.
Avoid full-repo scan unless required.

## Required workflow

1. Before coding, read `.aido/AI_CONTEXT.md`.
2. From `AI_CONTEXT.md`, choose only 1-2 relevant map files in `.aido/maps/`.
3. Read only source files listed in chosen map files.
4. Do not scan full repo unless:
   - `.aido` missing, or
   - `.aido` outdated, or
   - task cannot be understood from available maps.
5. After coding, update only relevant `.aido` files.
6. Keep `.aido` docs short, factual, AI-friendly.

## Outdated rules

Treat `.aido` as outdated when one or more applies:
- `AI_CONTEXT.md` contradicts current repo layout.
- map files reference missing or renamed files.
- task target area not represented in maps.
- `.aido/recent-changes.md` has no fresh entry for major recent work.

When outdated:
- perform smallest possible targeted scan to recover context.
- update only affected `.aido` docs.

## Read policy

- Prefer map-listed files over discovery scans.
- If map uses globs, expand only needed matches.
- Do not open unrelated files.
- Explain fallback reason when broader scan is unavoidable.

## Update policy after changes

Always do both when relevant:
- append one short line to `.aido/recent-changes.md`.
- update impacted map file(s) when file list/ownership changes.

Do not rewrite entire `.aido` set when only one area changed.

## Writing style for `.aido`

- Short sections.
- Concrete file paths.
- No long narrative.
- No marketing language.

## Map file pattern

Use this structure for each map:

```md
Description: One-line area summary.
files:
  - path/to/file.ext
  - path/to/dir/*.ext
why: One-line reason this map should be chosen.
```

## Quick execution checklist

1. Read `.aido/AI_CONTEXT.md`.
2. Pick 1-2 maps.
3. Read listed files only.
4. Implement change.
5. Update relevant `.aido` docs.
