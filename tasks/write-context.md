# Write Context Task

Generate the project's `CLAUDE.md` (and `AGENTS.md` symlink) from the interview answers and tool catalogue.

## Inputs

Receives the structured object from `tasks/interview.md`:
```
PROJECT_NAME, WHAT_BUILT, STACK, AGENT_ROLE, CONSTRAINTS, VERIFICATION_BAR
```

And the tool list from `tools.yaml` (already bootstrapped).

## Steps

1. Read `templates/claude-md.md` — the base template.
2. Fill in all `{{PLACEHOLDER}}` values using the interview answers.
3. Select which tools from `tools.yaml` to highlight based on the project stack and agent role:
   - GitHub/CLI work → emphasize `axi`
   - Browser automation → emphasize `agent-browser-axi`
   - Multi-agent / parallel work → emphasize `firstmate`
   - Any external library usage → emphasize `context7`
4. Write the filled template to `CLAUDE.md` in the current working directory.
5. Create `AGENTS.md` as a copy of `CLAUDE.md` (for OpenAI-compatible agents):
   ```bash
   cp CLAUDE.md AGENTS.md
   ```
6. Write `.gitignore` entries (append if file exists, create if not) — see list below.

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

- Don't overwrite an existing CLAUDE.md without warning the user first.
- `~/tools` is in the home directory — no need to gitignore it.
- If AGENTS.md already differs from CLAUDE.md (manually edited), warn rather than overwrite.
