---
name: project-init
description: Initialize a new project with agentic engineering context, shared tools, reusable skills, CLAUDE.md, and .gitignore. Use when starting a new project or setting up an existing repo for agent-assisted development. Triggers on /project-init, "initialize project", "set up project", or "bootstrap project".
---

# Project Init

Bootstraps a project for agentic engineering: installs shared tools to `~/tools`, copies reusable skills, interviews the user to write a tailored `CLAUDE.md` (and `AGENTS.md`), and sets up `.gitignore`.

Designed to be:
- **Agent-agnostic** — outputs work with Claude, GPT-based agents, or any system that reads `AGENTS.md` / `CLAUDE.md`
- **Easily extendable** — add tools to `tools.yaml`, add skills to `tasks/install-skills.md`, adjust the CLAUDE.md shape in `templates/claude-md.md`
- **Idempotent** — safe to re-run; pulls latest tools, refreshes skills, warns before overwriting context files

---

## Commands

| Command | What It Does |
|---------|-------------|
| `/project-init` | Full init: interview → tools → skills → context files |
| `/project-init tools` | Only bootstrap/update `~/tools` repos |
| `/project-init skills` | Only install/refresh project skills |
| `/project-init context` | Only (re)generate CLAUDE.md + AGENTS.md |

---

## Execution Order (full init)

Run these tasks in sequence. Each task file has full instructions.

### Step 1 — Interview
Read and execute `tasks/interview.md`.

Gather: project name, what's being built, stack, agent role, constraints, verification bar.

### Step 2 — Bootstrap Tools
Read and execute `tasks/bootstrap-tools.md`.

For each entry in `tools.yaml`: clone if missing, `git pull` if present. Report status.

### Step 3 — Install Skills
Read and execute `tasks/install-skills.md`.

Copy relevant skills from pi-builder (`~/code/pi-builder/skills/`) or global (`~/.claude/skills/`) into `.claude/skills/` in the current project.

### Step 4 — Write Context Files
Read and execute `tasks/write-context.md`.

Fill `templates/claude-md.md` with interview answers and tool catalogue. Write:
- `CLAUDE.md` — primary context file
- `AGENTS.md` — copy for OpenAI-compatible agents
- `.gitignore` — standard entries appended/created

---

## Extending This Skill

| What to change | Where |
|----------------|-------|
| Add/remove tools from `~/tools` | `tools.yaml` |
| Add/remove skills installed into projects | `tasks/install-skills.md` (skills table) |
| Change the shape of the generated CLAUDE.md | `templates/claude-md.md` |
| Add interview questions | `tasks/interview.md` |
| Change .gitignore defaults | `tasks/write-context.md` (.gitignore section) |

---

## Notes

- All task and template paths are relative to this skill's directory.
- `~/tools` is a shared directory across projects — never add it to a project `.gitignore`.
- On a new machine: the first run will clone all tools fresh. Subsequent runs pull updates.
- This skill itself lives in a GitHub repo — reference it from new projects rather than copying it.
