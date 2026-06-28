# Bootstrap Tools Task

Ensure all tools in `tools.yaml` are present, up-to-date, and fully installed in `~/tools`.

## Steps

1. Read `tools.yaml` (relative to this skill's directory) to get the full tool list.

2. Create `~/tools` if it doesn't exist:
   ```bash
   mkdir -p ~/tools
   ```

3. For each tool entry, clone or pull the repo:
   ```bash
   # Already cloned → pull latest
   if [ -d ~/tools/<repo-name> ]; then
     git -C ~/tools/<repo-name> pull --ff-only
   else
     git clone <url> ~/tools/<repo-name>
   fi
   ```
   Use the repo name (the part after `/`) as the directory name.

4. If the tool has an `install` field, run that command after the clone/pull — every time, not just on first clone. This ensures the globally installed package stays in sync with the repo. Run it regardless of whether this was a fresh clone or a pull.
   ```bash
   # example entries from tools.yaml:
   npm install -g gh-axi
   npm install -g chrome-devtools-axi
   pip install agent-reach
   npm install -g @upstash/context7-mcp
   # etc.
   ```

5. If the tool has `mcp: true`, after installing print a reminder:
   ```
   ⚠ MCP setup required: <repo-name>
   Add it to your agent's MCP config. See ~/tools/<repo-name>/README.md for the exact config block.
   ```

6. Report status for each tool:
   - ✓ Up to date + installed
   - ↓ Pulled N new commits + reinstalled
   - ⬇ Freshly cloned + installed
   - ⚠ Install step failed — show the error, continue with next tool

## Error Handling

- If a git pull fails (e.g. local changes, network error), warn and continue.
- If an install command fails, warn with the error output and continue — don't abort the whole init.
- Collect all warnings and print a summary at the end so the user can fix them in one go.

## Notes

- Run all clones/pulls sequentially to avoid git lock conflicts.
- `~/tools` is outside the project directory and should NOT be in the project's .gitignore.
- The tool paths and globally installed binaries will be referenced in the generated CLAUDE.md.
- On a new machine, first run clones everything fresh and installs all packages. Subsequent runs pull updates and reinstall to stay current.
