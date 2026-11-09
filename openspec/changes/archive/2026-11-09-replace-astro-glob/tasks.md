# Tasks

## 1. Replace the glob call

- [x] 1.1 In `src/components/Projects.astro`, replace `let PROJECTS = await Astro.glob('../pages/projects/*.md')` with `const PROJECTS = Object.entries(import.meta.glob('../pages/projects/*.md', { eager: true })).map(([, mod]) => mod)` and keep the existing sort/filter lines untouched; verify the file has no remaining `Astro.glob` reference (grep across `src/` returns zero matches)

## 2. Build verification

- [x] 2.1 Run `npm run build` and verify it exits 0 generating all 15 static routes including `/index.html` (the previously failing page); confirm no `Astro.glob is not a function` error appears
- [x] 2.2 Run `npm run dev` (or `npm run preview`) and verify the home page renders the visible project cards in the same order as before the change (`order` descending, `hidden: false` only)

## Workflow follow-up

- Archive the change after the build and page output are verified.
