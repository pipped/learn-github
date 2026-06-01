# How npm audit Works

When you install packages, those packages have their own dependencies — and any of them could have known security vulnerabilities. `npm audit` finds them.

---

## Step 1 — Run your first audit

Inside any Node.js project:

```bash
npm audit
```

If everything is fine:

```
found 0 vulnerabilities
```

If there are issues:

```
axios  1.0.0 - 1.15.2
Severity: high
axios Vulnerable to prototype pollution
fix available via `npm audit fix`
```

---

## Step 2 — Understand the output

Each vulnerability shows:

- **Package name** — which package has the issue
- **Affected versions** — the range of versions that are vulnerable
- **Severity** — low, moderate, high, or critical
- **Fix available** — whether updating it will solve it

The vulnerability might not be in a package you installed directly. It could be buried several layers deep:

```
your app
  └── axios          ← you installed this
        └── follow-redirects  ← this one is vulnerable
```

`npm audit` catches all of them.

---

## Step 3 — Fix the vulnerabilities

```bash
npm audit fix
```

This automatically updates packages to the nearest safe version without breaking anything. Run `npm audit` again after to confirm they're gone.

---

## Step 4 — When npm audit fix isn't enough

Sometimes a fix requires a major version bump (breaking change):

```
fix available via `npm audit fix --force`
Will install vite@8.0.15, which is a breaking change
```

`--force` allows the major version jump. Be careful — the new version may have changes that break your code.

If the breaking change isn't worth it right now, you can tell CI to only fail on serious issues:

```bash
npm audit --audit-level=high
```

This passes even if moderate vulnerabilities exist. Only high or critical issues will fail the build.

---

## Step 5 — Add it to CI

In your GitHub Actions workflow:

```yml
- run: npm audit --audit-level=high
```

Now every push is automatically scanned. If a package you depend on gets a new security issue reported, your next push will catch it.

---

## Key things to remember

- Vulnerabilities are usually in dependencies of your dependencies, not packages you installed directly
- `npm audit fix` handles most issues automatically
- `--force` is for breaking changes — check what changed before using it
- `--audit-level=high` lets you skip moderate issues that have no safe fix yet
