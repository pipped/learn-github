# How Vite Works

Vite is a build tool for frontend projects. It takes your source files (JSX, TypeScript, CSS) and turns them into plain HTML, JavaScript, and CSS that a browser can run.

---

## Step 1 — Understand the problem Vite solves

Browsers can't run JSX or modern JavaScript features like `import/export` across multiple files without help. You need a tool to:

1. Bundle all your files into one (or a few) optimised files
2. Convert JSX into plain JavaScript
3. Serve your app locally during development with instant updates

Vite does all three.

---

## Step 2 — Create a project with Vite

```bash
npm create vite@latest my-app
cd my-app
npm install
npm run dev
```

Vite will ask you to choose a framework — select **React**. After `npm run dev`, your app is running at `http://localhost:5173`.

---

## Step 3 — Understand the dev server

When you run `npm run dev`, Vite starts a local development server. Unlike older tools, Vite doesn't bundle all your files upfront. Instead it:

1. Serves files individually on demand
2. Converts only what the browser requests, right when it's requested
3. Uses the browser's native `import` support

This is why Vite starts almost instantly even on large projects — it doesn't process anything it doesn't need to yet.

---

## Step 4 — See Hot Module Replacement in action

Open your app in the browser, then edit a component. Vite updates just that component in the browser **without refreshing the page** — your state and scroll position stay the same.

This is called HMR (Hot Module Replacement). Vite pushes only the changed module to the browser instead of reloading everything.

---

## Step 5 — Build for production

```bash
npm run build
```

This creates a `dist/` folder containing your production-ready app:

```
dist/
  index.html
  assets/
    index-abc123.js    ← all your JavaScript bundled and minified
    index-def456.css   ← all your CSS bundled and minified
```

The filenames include a hash (e.g. `abc123`) so browsers know when to download a fresh version instead of using a cached one.

---

## Step 6 — Understand the config file

`vite.config.js` is where you configure Vite:

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [react()],
})
```

- `plugins: [react()]` — adds JSX support and React Fast Refresh (HMR for React components)
- You can add more plugins here for things like TypeScript path aliases, SVG imports, etc.

---

## Step 7 — Preview the production build

```bash
npm run preview
```

This serves the `dist/` folder locally so you can test the production build before deploying. Runs on `http://localhost:4173`.

Use this to catch issues that only appear in the production bundle — sometimes things behave differently when minified or tree-shaken.

---

## Key things to remember

- `npm run dev` — local dev server, fast startup, HMR, no bundling upfront
- `npm run build` — creates the `dist/` folder with your optimised production app
- `npm run preview` — serves the production build locally to test before deploying
- `dist/` should be in `.gitignore` — it's generated output, not source code
- Vite is a dev tool — it's not installed in production, only used to build the files you deploy
