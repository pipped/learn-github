# GitHub Basics

GitHub is where your git history lives online. It lets you share code, collaborate with others, and access your project from any machine.

---

## Step 1 — Create a repository on GitHub

1. Go to [github.com](https://github.com) and sign in
2. Click the **+** icon in the top right → **New repository**
3. Give it a name (e.g. `my-project`)
4. Choose **Public** (anyone can see it) or **Private** (only you)
5. Leave "Initialize this repository" unchecked if you already have code locally
6. Click **Create repository**

GitHub will show you commands to connect your local project to this new repo.

---

## Step 2 — Connect your local project to GitHub

After creating the repo, run these in your project folder:

```bash
git remote add origin https://github.com/yourusername/my-project.git
git branch -M main
git push -u origin main
```

- `remote add origin` — tells your local git where GitHub is. `origin` is just the conventional name for your main remote
- `branch -M main` — renames your branch to `main` (GitHub's default)
- `push -u origin main` — sends your commits to GitHub. The `-u` flag means future pushes only need `git push`

---

## Step 3 — Clone a repo to another machine

If you want to work on a project from a different computer:

```bash
git clone https://github.com/yourusername/my-project.git
cd my-project
```

This downloads the entire repo and its history to your machine. You're ready to make changes and push.

---

## Step 4 — Understand branches

A branch is a separate version of your code. The default branch is called `main`.

Create a new branch when you want to work on something without touching the main codebase:

```bash
git checkout -b my-feature
```

Now you're on a new branch. Any commits you make stay on `my-feature` and don't affect `main`.

To switch back to main:

```bash
git checkout main
```

To push your branch to GitHub:

```bash
git push -u origin my-feature
```

---

## Step 5 — Open a Pull Request

A Pull Request (PR) is how you propose merging one branch into another on GitHub.

1. Push your branch to GitHub
2. Go to your repo on GitHub — you'll see a banner saying your branch was recently pushed
3. Click **Compare & pull request**
4. Add a title and description explaining what you changed and why
5. Click **Create pull request**

GitHub will show the diff (exactly what changed) and let collaborators review it before it gets merged into `main`.

---

## Step 6 — Merge the Pull Request

Once the PR is reviewed and approved:

1. Click **Merge pull request** on GitHub
2. Click **Confirm merge**
3. Optionally delete the branch — it's no longer needed once merged

Pull your changes back locally:

```bash
git checkout main
git pull
```

---

## Step 7 — Stay up to date

If someone else pushed changes to the remote, pull them down:

```bash
git pull
```

This fetches the latest commits from GitHub and merges them into your current branch.

---

## Key things to remember

- **Repository (repo)** — your project and its entire history
- **Clone** — download a repo from GitHub to your machine
- **Branch** — an isolated version of the code to work on safely
- **Pull Request** — a proposal to merge one branch into another
- **Pull** — download the latest changes from GitHub to your local machine
- **Push** — send your local commits up to GitHub
