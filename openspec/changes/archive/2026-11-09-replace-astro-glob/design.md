# Design

## Context

With Astro 7, `Astro.glob()` no longer exists. The only usage in the codebase is `src/components/Projects.astro:3`, which loads the `.md` project pages under `src/pages/projects/` to render cards on the home page (sort by `frontmatter.order`, filter `hidden == false`, pass `frontmatter` + `url` to `ProjectCard`). See proposal.md - Why.

## Goals / Non-Goals

**Goals:**
- Restore the build on Astro 7 with the smallest possible diff.
- Preserve the exact rendered output: same cards, same order, same props.

**Non-Goals:**
- Migrating to Content Collections (deferred; see Decisions).
- Changing project page structure, frontmatter, or styling.

## Decisions

**Use `import.meta.glob('../pages/projects/*.md', { eager: true })` instead of Content Collections.**

- Rationale: the `.md` files stay where they are (they serve dual duty as routed pages under `src/pages/` and as data for the home page). A Vite glob returns each compiled Markdown module with `frontmatter` and `url` exports, exactly the surface `Astro.glob` used to provide, so the component body needs no restructuring. With `eager: true` there is no async boundary, matching the current top-level `await` idiomatics.
- Alternative considered: a glob-loader content collection (`src/content.config.ts` + `getCollection('projects')`). It adds frontmatter schema validation and typing, but the `.md` files live in `src/pages/`, so collecting from there would require either pointing the loader at page files (mixing routing and data concerns) or physically moving the files and handling rendering differently. That is a structural migration out of scope for an unblocking fix. Can be revisited later.

## Risks / Trade-offs

- [No frontmatter type validation] → Acceptable: frontmatter is stable and hand-maintained (10 files); a bad shape would surface at build time in `ProjectCard` just as today. Future content-collection migration would add validation.
- [`eager: true` builds all Markdown modules into the home-page module graph] → Same cost as the previous `Astro.glob` behavior; no regression.
- [Behavior difference between glob APIs for non-`.md` matches] → Pattern is restricted to `*.md` in a fixed directory, so no divergence.

## Open Questions

None.
