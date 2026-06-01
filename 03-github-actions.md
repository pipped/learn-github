# How GitHub Actions Works

GitHub Actions automatically runs tasks — like checking for errors or building your app — every time you push code. You set it up once and it runs forever.

---

## Step 1 — Understand what it does

Every time you push to GitHub, Actions can automatically:
- Check your code for errors (lint)
- Try to build your app
- Run tests
- Scan for security issues

If any step fails, GitHub marks the push with a red X so you know something broke.

---

## Step 2 — Create the workflow folder

GitHub looks for workflow files in one specific place:

```bash
mkdir -p .github/workflows
```

The folder name and location are the convention GitHub watches for. Change either one and GitHub won't find it.

---

## Step 3 — Create your first workflow file

Create `.github/workflows/ci.yml`:

```yml
name: CI

on:
  push:
    branches: [main]

jobs:
  check:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 24
      - run: npm install
      - run: npm run build
```

Break it down:
- `name` — what shows up in the GitHub Actions tab
- `on` — when to run it (on every push to main)
- `jobs` — the work to do
- `runs-on` — GitHub spins up a fresh Ubuntu virtual machine for each run
- `uses` — reusable actions published by GitHub (checkout clones your repo, setup-node installs Node)
- `run` — shell commands to execute

---

## Step 4 — Push it and watch it run

```bash
git add .github/workflows/ci.yml
git commit -m "Add CI workflow"
git push
```

Go to your repo on GitHub → click the **Actions** tab. You'll see the workflow running in real time.

---

## Step 5 — Read the results

Each step shows a green checkmark or red X:

```
✓ actions/checkout@v4
✓ actions/setup-node@v4
✓ npm install
✗ npm run build   ← something broke here
```

Click any step to see the full log output — the exact error message is in there.

---

## Step 6 — Add multiple jobs

Jobs run in parallel by default:

```yml
jobs:
  frontend:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: frontend
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 24
      - run: npm ci
      - run: npm run lint
      - run: npm run build

  backend:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: backend
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 24
      - run: npm ci
```

`defaults.run.working-directory` sets which folder the commands run in.

---

## Key things to remember

- Drop a `.yml` file in `.github/workflows/` and GitHub picks it up automatically — nothing to configure
- Each job gets a fresh virtual machine — nothing carries over between runs
- `npm ci` is preferred over `npm install` in CI because it installs exactly what's in the lock file
- The Actions tab on your repo shows every run and its full logs
