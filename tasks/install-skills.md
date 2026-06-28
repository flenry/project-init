# Install Skills Task

Copy reusable skills into the project's `.claude/skills/` directory.

## Skill Sources (in priority order)

1. **pi-builder** (`~/code/pi-builder/skills/`) — primary source
2. **Global Claude skills** (`~/.claude/skills/`) — fallback for skills not in pi-builder

## Skills to Install

| Skill | Source | When to install |
|-------|--------|-----------------|
| `seed` | pi-builder | always — project ideation |
| `paul` | pi-builder | always — plan-apply-unify loop |
| `autoexperiment` | pi-builder | always — autonomous experiment loop |
| `frontend-design` | pi-builder | if stack includes frontend/UI |
| `tdd` | global | always — test-driven development |
| `refactor` | global | always — structured refactors |

## Steps

1. Create `.claude/skills/` in the current working directory if it doesn't exist.

2. For each skill to install:
   - Check pi-builder source first: `~/code/pi-builder/skills/<skill>/`
   - Fall back to global: `~/.claude/skills/<skill>/`
   - If neither exists, skip and note it in the summary.

3. Copy the entire skill directory:
   ```bash
   cp -r <source>/<skill> .claude/skills/<skill>
   ```
   Overwrite if already present (keeps skills fresh on re-init).

4. Report what was installed, skipped, or missing.

## Adding More Skills

To add a skill to future project-inits, add a row to the table above with its source path. That's the only change needed — this task reads the table and acts on it.
