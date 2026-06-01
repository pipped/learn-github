# How Git Works

Git saves snapshots of your code over time so you can track changes and go back if something breaks.

---

## Step 1 — Create a folder and turn it into a git repo

```bash
mkdir my-project
cd my-project
git init
```

`git init` creates a hidden `.git` folder inside your project. That folder is where git stores all the history. Your code stays where it is.

---

## Step 2 — Create a file and check what git sees

```bash
echo "hello" > index.txt
git status
```

You'll see:

```
Untracked files:
  index.txt
```

Git can see the file exists but isn't tracking it yet.

---

## Step 3 — Stage the file

```bash
git add index.txt
git status
```

Now you'll see:

```
Changes to be committed:
  new file: index.txt
```

Staging means you're telling git "include this file in my next snapshot."

---

## Step 4 — Commit (save the snapshot)

```bash
git commit -m "Add index.txt"
```

This saves the snapshot permanently. The `-m` flag is the message describing what you did.

Check the history:

```bash
git log --oneline
```

You'll see something like:

```
4e0e155  Add index.txt
```

That `4e0e155` is the commit's unique ID called a SHA. Every commit gets one.

---

## Step 5 — Make a change and commit again

```bash
echo "world" >> index.txt
git add index.txt
git commit -m "Add second line"
git log --oneline
```

Now you have two commits:

```
9f3a2b1  Add second line
4e0e155  Add index.txt
```

This is your project history. You can go back to any point.

---

## Step 6 — Connect to GitHub and push

Go to github.com/new and create an empty repo, then:

```bash
git remote add origin https://github.com/yourusername/my-project.git
git branch -M main
git push -u origin main
```

- `remote add origin` — tells git where GitHub is
- `push -u origin main` — sends your commits up to GitHub

After this, every future push is just `git push`.

---

## Key things to remember

- **git** runs on your computer. **GitHub** is just a website that stores your git history online.
- A commit is permanent — you cannot edit it. You can only create a new one that replaces it.
- `git add` stages a file. `git commit` saves the snapshot. `git push` sends it to GitHub.
