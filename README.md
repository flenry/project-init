# project-init

Claude Code skill that bootstraps any project for agentic engineering.

## Install

```bash
git clone git@github.com:flenry/project-init.git .claude/skills/project-init
```

## Usage

Open Claude Code in the project directory and run:

```
/project-init
```

This will:
1. Interview you about the project (name, stack, constraints, verification bar)
2. Clone/pull shared tools into `~/tools`
3. Install reusable skills into `.claude/skills/`
4. Write `CLAUDE.md`, `AGENTS.md`, and `.gitignore`

## Subcommands

```
/project-init tools    # only update ~/tools
/project-init skills   # only refresh installed skills
/project-init context  # only regenerate CLAUDE.md + AGENTS.md
```

## Extending

| What to change | Where |
|----------------|-------|
| Add/remove tools | `tools.yaml` |
| Add/remove installed skills | `tasks/install-skills.md` |
| Change CLAUDE.md shape | `templates/claude-md.md` |
| Add interview questions | `tasks/interview.md` |
