# How ESLint Works

ESLint reads your code without running it and flags problems — like a spell checker for code. It catches bugs and enforces consistency before you even open a browser.

---

## Step 1 — Install ESLint

```bash
npm install eslint --save-dev
```

`--save-dev` means it's a development tool, not part of your actual app.

---

## Step 2 — Create a config file

Create `.eslintrc.cjs` in your project root:

```js
module.exports = {
  root: true,
  env: { browser: true, es2020: true },
  extends: ['eslint:recommended'],
}
```

- `root: true` — stops ESLint from looking in parent folders for more config
- `env` — tells ESLint what global variables exist (e.g. `window`, `document` in a browser)
- `extends` — which ruleset to use. `eslint:recommended` is a solid starting point

---

## Step 3 — Add a lint script to package.json

```json
"scripts": {
  "lint": "eslint . --ext js,jsx --max-warnings 0"
}
```

- `.` — check all files from the current folder
- `--ext js,jsx` — only check these file types
- `--max-warnings 0` — fail even on warnings, not just errors

---

## Step 4 — Run it

```bash
npm run lint
```

If there are problems you'll see:

```
src/App.jsx
  12:5  error  'myVar' is defined but never used  no-unused-vars
  24:1  error  Expected '===' but found '=='       eqeqeq

✖ 2 problems (2 errors, 0 warnings)
```

Each line shows:
- The file and line number
- The severity (error or warning)
- What's wrong
- Which rule caught it

---

## Step 5 — Understand rule severity

In your config you can set each rule to three levels:

```js
rules: {
  'no-unused-vars': 'error',    // fails the build
  'no-console': 'warn',         // shows a warning but passes
  'react/prop-types': 'off',    // disabled entirely
}
```

Turn off rules that don't apply to your project. For example, `react/prop-types` is disabled in projects that use TypeScript instead because TypeScript already handles type checking.

---

## Step 6 — Add it to CI

In your GitHub Actions workflow:

```yml
- run: npm run lint
```

Now every push is automatically checked. If someone commits code with unused variables or undefined values, the build fails and they're notified immediately.

---

## Key things to remember

- ESLint never runs your code — it only reads it, so it's instant
- The config file controls which rules are active
- `error` fails the build, `warn` passes with a note, `off` ignores it
- `--max-warnings 0` makes warnings behave like errors — keeps the codebase strict
