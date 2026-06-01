# How .gitignore Works

Some files should never be committed — passwords, secrets, or huge folders that anyone can regenerate. `.gitignore` tells git to skip them entirely.

---

## Step 1 — See the problem without .gitignore

```bash
mkdir my-project
cd my-project
git init
mkdir node_modules
echo "secret" > .env
git status
```

You'll see git wants to track everything:

```
Untracked files:
  .env
  node_modules/
```

You don't want either of these committed. `.env` has secrets. `node_modules` has thousands of files anyone can regenerate with `npm install`.

---

## Step 2 — Create a .gitignore file

```bash
echo "node_modules/" > .gitignore
echo ".env" >> .gitignore
```

Now run:

```bash
git status
```

You'll see:

```
Untracked files:
  .gitignore
```

`node_modules/` and `.env` are gone from the list. Git is pretending they don't exist. The files are still on your disk — git just ignores them.

---

## Step 3 — Understand the patterns

Open `.gitignore` and add more patterns:

```
node_modules/    # ignore an entire folder
.env             # ignore a specific file
*.log            # ignore any file ending in .log
dist/            # ignore build output
.claude/         # ignore a local notes folder
```

The `#` symbol is a comment — git ignores that line.

---

## Step 4 — Commit the .gitignore itself

```bash
git add .gitignore
git commit -m "Add .gitignore"
```

The `.gitignore` file gets committed so everyone working on the project uses the same rules.

---

## Step 5 — The important rule: order of operations

`.gitignore` only works on files git has never tracked before.

If you accidentally commit a file first:

```bash
git add .env
git commit -m "oops"
```

Adding `.env` to `.gitignore` afterwards won't help — git is already tracking it.

To fix it, you need to tell git to stop tracking it without deleting it:

```bash
git rm --cached .env
git commit -m "Remove .env from tracking"
```

Now add `.env` to `.gitignore` and commit that too.

---

## Key things to remember

- Files in `.gitignore` still exist on your disk — git just can't see them
- Always add a file to `.gitignore` before you commit it
- If you already committed it, use `git rm --cached` to untrack it
