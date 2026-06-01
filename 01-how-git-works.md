# How Git Works

## What is git

Git tracks the history of your code. Every time you commit, git saves a snapshot of your files at that moment. You can go back to any snapshot at any time.

## Commits

A commit is a saved snapshot. Each one has:
- A unique ID (called a SHA) like `4e0e155`
- A message describing what changed
- A pointer to the previous commit

This chain of commits is your project history.

```
2d07746  Build AI transcribe portfolio MVP
   ↓
01f23f9  Add backend and project docs
   ↓
4e0e155  Fix security vulnerabilities
   ↓
cb6ec05  Add CI workflow
```

## Commits are immutable

You cannot edit a commit once it exists. If you want to change a commit message or remove something from a commit, git creates a brand new commit with a new SHA and replaces the old one. The old one is discarded.

This is what happened when we removed the Co-Authored-By line — git rewrote the commits with new SHAs.

## git push vs git push --force

A regular `git push` only works if your local history extends the remote history (i.e. you just added new commits on top).

If you rewrote history (changed existing commits), the SHAs no longer match and git will reject a regular push. `--force` tells git to overwrite the remote with your local version regardless.

It's destructive — use it carefully on shared repos.

## git vs GitHub

- **git** — the tool that runs on your computer and tracks history
- **GitHub** — a website that hosts your repo online so others can see it and you can access it from any machine

Git works without GitHub. GitHub is just a remote storage location for your git history.
