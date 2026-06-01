# ESLint

## What it is

ESLint is a linter — a tool that reads your code without running it and flags problems. Think of it like a spell checker for code.

## What it catches

**Actual bugs**
- Using a variable before it's defined
- Unreachable code after a `return`
- Missing dependencies in a React `useEffect`

**Style and consistency**
- Unused imports or variables
- Using `==` instead of `===`
- Code that will cause issues in specific environments

## How it works

ESLint runs statically — it never executes your code, it just reads it. This means it runs instantly and doesn't need a server, database, or any external dependencies.

```bash
npm run lint
```

## The config file

`.eslintrc.cjs` tells ESLint which rules to apply:

```js
module.exports = {
  extends: [
    'eslint:recommended',           // ESLint's built-in rules
    'plugin:react/recommended',     // React-specific rules
    'plugin:react-hooks/recommended', // Rules for useEffect, useState, etc.
  ],
  rules: {
    'react/prop-types': 'off',      // disable a specific rule
  },
}
```

Each rule can be set to:
- `'error'` — fails the build
- `'warn'` — passes but shows a warning
- `'off'` — disabled entirely

## Why --max-warnings 0

The lint command in this project uses `--max-warnings 0`, which means even warnings fail the build. This keeps the codebase strict — warnings don't quietly accumulate.

## ESLint vs TypeScript

ESLint catches runtime patterns and style issues. TypeScript catches type mismatches. They complement each other — most serious projects use both. The `react/prop-types` rule was disabled because TypeScript is the modern way to type-check React components and prop-types adds unnecessary boilerplate.
