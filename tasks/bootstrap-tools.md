# Bootstrap Tools Task

Ensure all tools in `tools.yaml` are present and up-to-date in `~/tools`.

## Steps

1. Read `tools.yaml` (relative to this skill's directory) to get the tool list.

2. Create `~/tools` if it doesn't exist:
   ```bash
   mkdir -p ~/tools
   ```

3. For each tool entry, check if the directory exists:
   ```bash
   # Already cloned → pull latest
   if [ -d ~/tools/<repo-name> ]; then
     git -C ~/tools/<repo-name> pull --ff-only
   else
     # Fresh clone
     git clone <url> ~/tools/<repo-name>
   fi
   ```
   Use the repo name (the part after `/`) as the directory name.

4. Report status for each tool:
   - ✓ Already up to date
   - ↓ Pulled N new commits
   - ⬇ Freshly cloned

5. If a pull fails (e.g. local changes, network error), warn the user and continue — don't abort the whole init.

## Notes

- Run all clones/pulls sequentially to avoid git lock conflicts.
- `~/tools` is outside the project directory and should NOT be in the project's .gitignore (it lives in home).
- The tool paths will be referenced in the generated CLAUDE.md so agents know where to find them.
