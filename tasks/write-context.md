# Write Context Task

Generate the project's `CLAUDE.md` (and `AGENTS.md`) from the interview answers and tool catalogue.

## Inputs

Receives the structured object from `tasks/interview.md`:
```
PROJECT_NAME, WHAT_BUILT, STACK, AGENT_ROLE, CONSTRAINTS, VERIFICATION_BAR
```

And the tool list from `tools.yaml` (already bootstrapped).

## Steps

1. Read `templates/claude-md.md` in full. This is the required output structure — do not substitute a shorter or custom version.
2. Fill in every `{{PLACEHOLDER}}` using the interview answers. If the user left something as TBD, write "TBD" — do not remove the section.
3. For the `{{#if VERIFICATION_BAR}}` blocks: keep the block matching the user's answer, remove the other two blocks entirely.
4. Keep ALL tool sections intact regardless of project type. Every project benefits from the shared toolset. Do not drop sections because "this project doesn't use agents."
5. Write the completed template to `CLAUDE.md`.
6. Copy to `AGENTS.md`:
   ```bash
   cp CLAUDE.md AGENTS.md
   ```
7. Write `.gitignore` entries (append if file exists, create if not) — see list below.

## .gitignore Entries to Add

```gitignore
# Environment
.env
.env.*
!.env.sample

# Agent scratch space
.scratch/
.tmp/

# OS
.DS_Store
Thumbs.db

# Editor
.vscode/
.idea/

# Logs
*.log
logs/
```

## Notes

- **Never write a custom or shortened CLAUDE.md.** The template structure must be preserved so future agents have complete context.
- Don't overwrite an existing CLAUDE.md without warning the user first.
- `~/tools` is in the home directory — no need to gitignore it.
- If AGENTS.md already differs from CLAUDE.md (manually edited), warn rather than overwrite.
