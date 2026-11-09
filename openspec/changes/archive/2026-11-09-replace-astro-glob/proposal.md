# Proposal

## Why

The build fails on the home page (`/`) with `TypeError: Astro.glob is not a function`. The project already runs Astro 7.4.8 (latest), but `src/components/Projects.astro` still calls `Astro.glob()`, an API that was removed in Astro 7. Every other route builds fine; this is the single blocker keeping the site from building.

## What Changes

- Replace `await Astro.glob('../pages/projects/*.md')` in `src/components/Projects.astro` with Vite's `import.meta.glob(..., { eager: true })`, which is supported in Astro 7.
- Keep the existing sorting (`frontmatter.order`) and filtering (`frontmatter.hidden == false`) logic unchanged.
- No changes to the `.md` project pages, `ProjectCard`, layouts, or any other file.

## Capabilities

### New Capabilities

<!-- None: pure refactor, no spec-level behavior change (skip_specs: true). -->

### Modified Capabilities

<!-- None. The rendered output (project cards sorted by order, hidden ones filtered out) is identical; only the internal globbing mechanism changes. -->

## Impact

- **Code:** `src/components/Projects.astro` (1 line changed, plus how the module list is unwrapped).
- **Build:** resolves the `Astro.glob is not a function` error so `npm run build` completes and `/` renders the 10 visible project cards.
- **Dependencies:** none added or removed.
- **Validation:** `npm run build` must exit 0 generating all 15 static routes.
