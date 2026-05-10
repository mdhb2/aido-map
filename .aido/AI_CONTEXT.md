Project: <project-name>
Purpose: Short one-line summary of product and codebase.
Primary langs: <e.g., TypeScript, Python>
Primary entrypoints:
  - <path/to/main/entrypoint>
  - <path/to/secondary/entrypoint>

How to use:
1. Read this file first.
2. Pick only 1-2 relevant maps from `.aido/maps/`.
3. Read only source files listed in selected maps.
4. Avoid full-repo scan unless `.aido` missing/outdated or task unclear.

Map index:
  - Only include map files that exist and contain at least one concrete file path for this repository.
  - Example: .aido/maps/api.md (only if it lists files present in this repo)

Outdated signals:
  - map path no longer exists
  - task area not covered by maps
  - major repo changes not reflected in `.aido/recent-changes.md`

Rules:
  - keep docs short and factual
  - update only relevant `.aido` files after coding
