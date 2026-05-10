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
