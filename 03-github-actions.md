# GitHub Actions

## What it is

GitHub Actions is a CI (continuous integration) system built into GitHub. It automatically runs tasks — like tests, linting, or builds — whenever you push code.

## How it works

GitHub watches your repo for `.yml` files inside `.github/workflows/`. When you push a commit, GitHub reads those files and executes whatever steps are defined.

```
You push a commit
      ↓
GitHub detects .github/workflows/ci.yml
      ↓
GitHub spins up a fresh virtual machine on their servers
      ↓
That VM clones your repo
      ↓
Runs each step (npm install, lint, build, etc.)
      ↓
Reports pass or fail
      ↓
VM is destroyed
```

You don't manage any servers. The runner is GitHub's infrastructure.

## The yml file

```yml
name: CI

on:
  push:
    branches: [main]      # run when you push to main
  pull_request:
    branches: [main]      # run when a PR targets main

jobs:
  frontend:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4     # clones your repo onto the VM
      - uses: actions/setup-node@v4   # installs Node.js
        with:
          node-version: 24
      - run: npm ci                   # install dependencies
      - run: npm run lint             # run lint
      - run: npm run build            # run build
```

## Reusable actions

Lines like `actions/checkout@v4` are pre-built actions published by GitHub at github.com/actions/checkout. The `@v4` pins to a specific version so your workflow doesn't break if the action updates.

## Free tier

Public repos get unlimited minutes. Private repos get 2,000 free minutes per month. Each run on this project takes under 2 minutes, so you'd never come close to the limit.

## Viewing results

Go to your repo on GitHub → Actions tab. Every run shows which steps passed or failed and the full log output.
