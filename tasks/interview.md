# Interview Task

Gather just enough context to write a useful CLAUDE.md. Keep it conversational — one topic at a time, not a form dump.

## Questions to Cover

Ask these in order, adapting naturally based on prior answers. Skip any that were already answered in the user's initial message.

1. **Project name** — what do we call this?
2. **What you're building** — one paragraph: the problem, who it's for, what it does
3. **Stack** — languages, frameworks, runtimes, databases (or "TBD" is fine)
4. **Agent role** — what will AI agents primarily do in this project? (e.g. write features, run evals, manage infra, data analysis, etc.)
5. **Key constraints** — anything non-negotiable? (e.g. "must use Postgres", "no external APIs", "output must be deterministic")
6. **Verification bar** — how strict? (prototype / feature in a live codebase / production system with CI gates)

## Output

Collect answers into a structured object you'll pass to `tasks/write-context.md`:

```
PROJECT_NAME: ...
WHAT_BUILT: ...
STACK: ...
AGENT_ROLE: ...
CONSTRAINTS: ...
VERIFICATION_BAR: prototype | structured | production
```
