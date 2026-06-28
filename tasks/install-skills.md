# Install Skills Task

Copy reusable skills into the project's `.claude/skills/` directory.

## Skill Sources (in priority order)

1. **pi-builder** (`~/code/pi-builder/skills/`) — primary source
2. **Global Claude skills** (`~/.claude/skills/`) — fallback for skills not in pi-builder
3. **workflows** (`~/tools/workflows/`) — role-based workflow skills (cloned via tools.yaml)
4. **project-guide** (`~/tools/project-guide/`) — guide skill (cloned via tools.yaml)

## Skills to Install

| Skill | Source | When to install |
|-------|--------|-----------------|
| `seed` | pi-builder | always — project ideation |
| `paul` | pi-builder | always — plan-apply-unify loop |
| `autoexperiment` | pi-builder | always — autonomous experiment loop |
| `frontend-design` | pi-builder | if stack includes frontend/UI |
| `tdd` | global | always — test-driven development |
| `refactor` | global | always — structured refactors |
| `bug` | global | always — triage bugs, file GitHub issues |
| `design-interface` | global | always — parallel interface design comparison |
| `interrogate` | global | always — stress-test plans and designs |
| `prd` | global | always — turn conversation into a PRD |
| `slice` | global | always — break PRD into shippable GitHub issues |
| `glossary` | global | always — extract domain language glossary |
| `setup-ts` | global | if stack includes TypeScript |
| `chat` | workflows | always — structured brainstorm, no implementation |
| `research` | workflows | always — multi-pass research with validation |
| `board-prd` | workflows | always — thorough PRD with architecture review |
| `build` | workflows | always — full TDD build with eval loop |
| `cr` | workflows | always — scoped change request with PR |
| `full-test` | workflows | always — PRD-driven QA with verdict |
| `guide` | project-guide | always — catalogue of all installed skills and tools |

## Steps

1. Create `.claude/skills/` in the current working directory if it doesn't exist.

2. For each skill to install:
   - Check pi-builder source first: `~/code/pi-builder/skills/<skill>/`
   - Fall back to global: `~/.claude/skills/<skill>/`
   - For workflows skills: copy from `~/tools/workflows/<skill>/`
   - For guide: copy from `~/tools/project-guide/`
   - If source not found, skip and note it in the summary.

3. Copy the entire skill directory:
   ```bash
   cp -r <source>/<skill> .claude/skills/<skill>
   ```
   Overwrite if already present (keeps skills fresh on re-init).

4. Report what was installed, skipped, or missing.

## Adding More Skills

To add a skill to future project-inits, add a row to the table above with its source path. That's the only change needed — this task reads the table and acts on it.
