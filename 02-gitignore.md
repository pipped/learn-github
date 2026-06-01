# .gitignore

## What it does

`.gitignore` is a file that tells git to ignore certain files or folders. Anything matching a pattern in `.gitignore` is invisible to git — it won't show up in `git status`, and `git add` won't pick it up.

The files still exist on your disk. Git just pretends they aren't there.

## Common patterns

```
node_modules/    # ignore an entire folder
.env             # ignore a specific file (usually contains secrets)
*.log            # ignore any file ending in .log
dist/            # ignore build output
.claude/         # ignore a folder with local notes
```

## Why it matters

Some files should never be committed:
- `node_modules/` — hundreds of MB of dependencies, anyone can regenerate them with `npm install`
- `.env` — contains passwords and API keys, committing these is a security risk
- `dist/` — compiled build output, generated from source code

## Important rule

`.gitignore` only works on files git has never tracked. If you commit a file first and then add it to `.gitignore`, git will keep tracking it.

To stop tracking a file that was already committed:
```bash
git rm --cached <filename>
```

This removes it from git's tracking without deleting it from your disk. Then commit the change.

## Order of operations

Always add a file to `.gitignore` before you commit it. That's the safe order.
