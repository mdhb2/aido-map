# aido-map

Token-saving OpenCode skill to guide AI agents to read repo index in `.aido/` before scanning source. Keeps documentation short, factual, and machine-friendly.

## Install

1. Download `aido-map.skill` from releases.

Example (manual):

```powershell

## Usage

When asking the assistant to perform repo-level tasks, the skill will:

- Read `.aido/AI_CONTEXT.md` first.
- Select 1-2 maps from `.aido/maps/`.
- Read only files listed in chosen maps.
- Avoid scanning entire repo unless `.aido` missing/outdated or task unclear.

After making changes, the assistant updates `.aido/recent-changes.md` and relevant maps only.

## Files included

- `SKILL.md` — skill instructions and trigger description
- `.aido/` — templates and maps for indexing repo
- `evals/evals.json` — sample eval prompts
- `aido-map.skill` — packaged archive

## Trigger tuning

If you want to optimize skill trigger behavior, create a trigger eval set and run your platform's optimization loop. See `aido-map/trigger_evals.json` for sample queries.
