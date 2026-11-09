# Design

## Context

`@tailwindcss/vite` only processes CSS reachable from the module graph. `public/` assets are served verbatim, so the Tailwind v4 directives added there never compile. See proposal.md - Why.

## Goals / Non-Goals

**Goals:**
- Tailwind (utilities + typography + dark variant) and the project's custom CSS compile and load again, with one single source of truth.
- No behavioral changes to markup, components, or class names.

**Non-Goals:**
- Refactoring or redesigning the custom CSS rules.
- Removing the boxicons CDN link or any third-party asset.

## Decisions

**Move the entry (and `fonts.css`) under `src/styles/` and import it from layouts, instead of creating a new synthesized entry.**

- Rationale: the file already contains everything (directives + tokens + custom classes) and the layouts are its only consumers. A single `import "../styles/main.css"` in each layout keeps the diff auditable: same rules, new home.
- Alternative considered: wrapping the minified custom rules inside layers or splitting per-component CSS — more churn, no benefit for this fix.

`@custom-variant dark (&:where(.dark, .dark *));` remains as-is (it is a source directive Tailwind compiles, matching the `.dark` toggling used by `SwitchTheme`).

## Risks / Trade-offs

- [Browser-cached stale `/assets/css/main.css?v=1`] → The URL disappears entirely; hard-refresh clears it. `?v=1` was a manual cache-buster that stops being needed since Vite fingerprints the emitted asset.
- [`@import "fonts.css"` resolving differently under Vite] → Keep both files side by side in `src/styles/` and use the relative form Vite resolves at build (`@import "./fonts.css"`), so fonts keep loading.
- [Missed consumer of the deleted public URL] → Only the two layouts link it today (grep-verified); no JS or component references `/assets/css/main.css`.

## Open Questions

None.
