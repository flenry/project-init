# {{PROJECT_NAME}}

## What We're Building

{{WHAT_BUILT}}

## Stack

{{STACK}}

## Agent Role in This Project

{{AGENT_ROLE}}

## Constraints

{{CONSTRAINTS}}

---

## Agentic Engineering Principles

This project follows structured agentic engineering, not vibe coding.

**The distinction:** outputs are verified systematically, not manually spot-checked.

### Verification Bar: {{VERIFICATION_BAR}}

{{#if VERIFICATION_BAR == "production"}}
- All PRs must pass automated tests + CI gates before merge
- Code review: AI first-pass for bugs/style, human for architecture
- Evals required for any non-deterministic agent output
- Continuous monitoring in production; automated rollback on failure
{{/if}}
{{#if VERIFICATION_BAR == "structured"}}
- Tests must pass before committing
- Human review at architectural decision points
- Basic evals for agent trajectories
{{/if}}
{{#if VERIFICATION_BAR == "prototype"}}
- Manual checks are acceptable; move fast
- Add tests before promoting to production
{{/if}}

---

## Context Engineering

Quality of agent output depends on context quality, not prompt cleverness.

**Static context** (this file — loaded every session): core mission, universal rules, non-negotiable constraints.

**Dynamic context** (skills, RAG, tool results — loaded on demand): specialized procedures, large reference material.

Keep this file lean. Move conditional knowledge to `.claude/skills/`.

---

## Tools & Best Practices

All shared tools live in `~/tools`. Run `git -C ~/tools/<name> pull` to update any of them.

### AXI — Agent-Ergonomic CLI (`~/tools/axi`)

Use AXI tools instead of raw Bash/CLI calls wherever available. AXI outputs are designed for agents: structured, token-efficient (~40% cheaper than standard CLIs), and unambiguous.

**For GitHub operations** — prefer AXI's GitHub tools over raw `gh` or `git` calls:
```bash
# Instead of: gh pr list
~/tools/axi/github pr-list

# Instead of: gh issue create ...
~/tools/axi/github issue-create --title "..." --body "..."
```

Check `~/tools/axi/README.md` for the full command catalogue before reaching for `gh` or `git` directly.

### Context7 — Live Library Docs (`~/tools/context7`)

Before using any external library, fetch its current docs via Context7 (MCP server). Avoids hallucinated API usage.

Setup: add Context7 as an MCP server in your agent config. See `~/tools/context7/README.md`.

### Firstmate — Multi-Agent Orchestration (`~/tools/firstmate`)

For parallel workstreams (multiple features, agents running concurrently), use Firstmate to dispatch work to isolated git worktrees and consolidate results. See `~/tools/firstmate/README.md`.

### Agent Browser AXI — Browser Automation (`~/tools/agent-browser-axi`)

Token-efficient browser automation for agents. Use instead of Playwright/Puppeteer when an agent needs to interact with a browser. See `~/tools/agent-browser-axi/README.md`.

---

## Skills Available

Project skills live in `.claude/skills/`. Load them on-demand — don't pre-load all of them.

| Skill | Trigger |
|-------|---------|
| `seed` | Starting a new sub-project or feature from a vague idea |
| `paul` | Structured plan → apply → unify loop for any unit of work |
| `autoexperiment` | Autonomous parameter tuning or iterative experiment loops |
| `frontend-design` | Building UI components or pages with high design quality |
| `tdd` | Test-driven feature development |
| `refactor` | Safe, incremental refactors broken into working commits |

---

## Key Rules

1. **Context over prompts** — write rich context, not clever one-liners
2. **Verification is mandatory** — tests + evals, not optional
3. **Use AXI for CLI tools** — fewer tokens, less ambiguity
4. **Load skills on demand** — don't bloat the session context
5. **Feedback loops over human interrupts** — route failures back to agents
6. **Human judgment on architecture** — agents implement; humans decide trade-offs

---

## References

- Agentic Engineering principles: Kun Chen's L8 workflow + Google's SDLC framework
- Tool docs: `~/tools/<name>/README.md`
- Skill docs: `.claude/skills/<name>/SKILL.md`
