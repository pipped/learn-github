# npm audit

## What it is

`npm audit` scans your project's dependencies for known security vulnerabilities. It checks every package in `node_modules` against a public database of reported issues.

```bash
npm audit
```

## What the output means

```
axios  1.0.0 - 1.15.2
Severity: high
axios Vulnerable to prototype pollution
fix available via `npm audit fix`
```

- **Severity** — low, moderate, high, or critical
- **Affected versions** — the range of versions that have the issue
- **Fix available** — whether updating the package resolves it

## Fixing vulnerabilities

```bash
npm audit fix
```

This automatically updates packages to the nearest safe version that doesn't break anything.

```bash
npm audit fix --force
```

This allows breaking changes (major version bumps). Use carefully — it may require code changes to work with the new version.

## Audit levels

You can tell `npm audit` to only fail on certain severities:

```bash
npm audit --audit-level=high
```

This passes even if there are moderate vulnerabilities. Useful in CI when a moderate issue has no fix available (like the esbuild/vite issue in ai-transcribe that would require a breaking Vite upgrade to resolve).

## Transitive dependencies

Most vulnerabilities aren't in packages you installed directly — they're in packages that your packages depend on. For example:

```
axios → follow-redirects (vulnerable)
express → qs (vulnerable)
```

`npm audit fix` handles these too, updating the nested dependency to a safe version.

## In CI

Running `npm audit` in GitHub Actions means every push is checked for new vulnerabilities. If a package you depend on gets a new CVE reported, your next push will catch it automatically.
