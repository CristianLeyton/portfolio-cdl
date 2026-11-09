# Proposal

## Why

After the Tailwind v4 migration, styles are broken: the Tailwind entry directives (`@import "tailwindcss"`, `@plugin "@tailwindcss/typography"`, `@custom-variant dark ...`) were added to `public/assets/css/main.css`, but files under `public/` are copied verbatim and never processed by Vite. The browser receives unresolvable `@import "tailwindcss"`, so zero Tailwind utilities (and no preflight) load, while every `.astro` component relies on utility classes. Before the migration the old `@astrojs/tailwind` integration injected compiled Tailwind v3 automatically, which masked this.

## What Changes

- Move the Tailwind entry CSS (`main.css` + its `fonts.css` dependency) from `public/assets/css/` to `src/styles/`, keeping all existing directives and rules intact (adjusting `@import` to a relative module path).
- Ownership of Tailwind compilation moves to the Astro/Vite module graph: both layouts import the entry CSS in their frontmatter instead of linking `/assets/css/main.css?v=1`.
- **BREAKING (internal):** the URL `/assets/css/main.css?v=1` no longer exists; the stylesheet is served as a Vite fingerprinted asset. Only the two layouts referenced it.

## Capabilities

### New Capabilities

<!-- None: this restores the pre-migration styling behavior; pure build/config fix (skip_specs: true). -->

### Modified Capabilities

<!-- None: no spec-level behavior change; the rendered styles return to their intended state. -->

## Impact

- **Code:** new `src/styles/main.css` + `src/styles/fonts.css`; `src/layouts/MainLayout.astro` and `src/layouts/CVLayout.astro` (remove `<link>`, add frontmatter `import "./../styles/main.css"`); deletion of `public/assets/css/main.css` and `fonts.css`.
- **Build:** `@tailwindcss/vite` compiles utilities, typography plugin, dark variant, and custom tokens into the emitted stylesheet.
- **Validation:** `npm run build` exits 0; served HTML references the bundled CSS; served CSS contains compiled Tailwind utilities (e.g. `.flex`) and the custom classes (`.card-proyecto`, `.navlink`, `.pill--primary`).
