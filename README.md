# aido-map

Token-saving OpenCode skill. Guide AI agent to read repo index in `.aido/` before scanning source. Docs short, factual, machine-friendly.

## Install (always latest)

Install uses latest release by default. No version required.

Windows PowerShell (download + extract latest):

```powershell
# download latest release asset
curl -L -o aido-map.skill "https://github.com/mdhb2/aido-map/releases/latest/download/aido-map.skill"
# extract to local folder
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.agents\skills\aido-map"
Expand-Archive -LiteralPath aido-map.skill -DestinationPath "$env:USERPROFILE\.agents\skills\aido-map" -Force
# verify
Get-ChildItem "$env:USERPROFILE\.agents\skills\aido-map" -Recurse
```

macOS / Linux (bash):

```bash
# download latest release asset
curl -L -o aido-map.skill "https://github.com/mdhb2/aido-map/releases/latest/download/aido-map.skill"
mkdir -p ~/.agents/skills/aido-map
unzip -o aido-map.skill -d ~/.agents/skills/aido-map
ls -la ~/.agents/skills/aido-map
```

Using GitHub CLI (authenticated) to fetch latest:

```bash
gh release download --repo mdhb2/aido-map --latest --pattern "aido-map.skill"
mkdir -p ~/.agents/skills/aido-map
unzip -o aido-map.skill -d ~/.agents/skills/aido-map
```

Install by cloning (user or project-local):

```bash
# install for current user
git clone https://github.com/mdhb2/aido-map.git ~/.agents/skills/aido-map

# or install into project (repo root)
mkdir -p .agents/skills
git clone https://github.com/mdhb2/aido-map.git .agents/skills/aido-map
```

Install using npx (one-liner)

If your environment supports the `skills` CLI via npx, install the skill in one command. This fetches the repo and installs the skill for OpenCode (or compatible agent platforms):

```bash
npx skills add https://github.com/mdhb2/aido-map --skill aido-map -a opencode
```

Notes:
- Replace URL or `--skill` value if you maintain a different fork or skill-name.
- This command installs latest by default.

## Usage

- Skill reads `.aido/AI_CONTEXT.md` first.
- Skill selects 1-2 maps from `.aido/maps/`.
- Skill reads only files listed in chosen maps.
- Skill avoids scanning full repo unless `.aido` missing/outdated or task unclear.

After changes, skill updates `.aido/recent-changes.md` and only relevant maps.

## How to use this skill (examples)

Example 1 — Ask for plan without changing code:

User prompt:
```
Please design GET /users/summary endpoint. Use repo index first and list which files you will open.
```

What skill does:
- Reads `.aido/AI_CONTEXT.md`.
- Picks 1-2 maps (e.g., `api.md`).
- Reads only files listed in chosen map.
- Outputs: list of files it will open, short implementation plan, and a unified patch diff suggestion.

Example 2 — Ask for fix and patch file:

User prompt:
```
There's a failing test in auth refresh tokens. Inspect and provide patch.
```

What skill does:
- Reads `.aido/AI_CONTEXT.md`.
- Picks `auth.md` map.
- Reads files listed in `auth.md`.
- Outputs: diagnosis, minimal patch diff, and a recommended `.aido/recent-changes.md` entry.

Example 3 — If `.aido` missing or outdated:

User prompt:
```
Add feature X that interacts with database.
```

What skill does:
- Detects `.aido` missing/outdated.
- Runs minimal targeted discovery inside repo to find candidate files (no blind full-repo scan).
- Creates or updates `.aido/maps` with concrete file lists and writes one-line entries to `.aido/recent-changes.md`.
- Outputs: discovery summary and suggested map entries for review.

Outputs you will see from the skill:
- `plan`: short bullet plan of what will change.
- `files_opened`: list of concrete file paths agent read.
- `patch`: unified diff patch suggestion (text) for small edits.
- `aido_updates`: recommended `.aido/recent-changes.md` lines and map edits (if applicable).


## Files included

- `SKILL.md` — skill instructions & trigger description
- `.aido/` — templates and maps for indexing repo
- `evals/evals.json` — sample eval prompts
- `aido-map.skill` — packaged archive

## Troubleshoot

- Skill not visible: ensure files under `~/.agents/skills/aido-map` or `%USERPROFILE%\.agents\skills\aido-map` and restart agent.
- Private repo releases: use `gh release download --repo mdhb2/aido-map --latest --pattern "aido-map.skill"` with auth.

## Update to latest

Keep skill installation up-to-date by downloading latest release and replacing installed files.

Windows PowerShell:

```powershell
# download latest release asset
curl -L -o aido-map.skill "https://github.com/mdhb2/aido-map/releases/latest/download/aido-map.skill"
# extract over existing installation
Expand-Archive -LiteralPath aido-map.skill -DestinationPath "$env:USERPROFILE\.agents\skills\aido-map" -Force
# restart agent or reload skills as required by your platform
```

macOS / Linux (bash):

```bash
# download latest release asset
curl -L -o aido-map.skill "https://github.com/mdhb2/aido-map/releases/latest/download/aido-map.skill"
unzip -o aido-map.skill -d ~/.agents/skills/aido-map
# restart agent or reload skills as required by your platform
```

GitHub CLI (authenticated):

```bash
gh release download --repo mdhb2/aido-map --latest --pattern "aido-map.skill"
unzip -o aido-map.skill -d ~/.agents/skills/aido-map
# or if installed via git clone
cd ~/.agents/skills/aido-map && git pull origin main
```

Notes:
- When updating, prefer replacing files in-place rather than creating duplicate skill folders.
- After update, restart OpenCode agent process or reload skill cache so new SKILL.md is picked up.

Update using npx skills (one-liner)

If your environment provides the `skills` CLI via npx, you can update or install the latest skill with a single command. This is idempotent: running the command again will fetch the latest release and replace the installed files.

```bash
npx skills add https://github.com/mdhb2/aido-map --skill aido-map -a opencode
```

If your `skills` CLI supports an explicit update command, you can use that instead:

```bash
npx skills update https://github.com/mdhb2/aido-map --skill aido-map -a opencode
```

Note: when installed via git clone, update with `git pull origin main` inside the skill folder instead.
