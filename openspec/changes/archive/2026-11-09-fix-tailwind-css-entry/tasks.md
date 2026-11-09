# Tasks

## 1. Move Tailwind entry into the module graph

- [x] 1.1 Create `src/styles/main.css` with the current content of `public/assets/css/main.css`, changing `@import "fonts.css"` to `@import "./fonts.css"`; move `public/assets/css/fonts.css` to `src/styles/fonts.css` unchanged; verify both `src/styles/*.css` exist and `public/assets/css/` only holds non-CSS assets it may still own
- [x] 1.2 In `src/layouts/MainLayout.astro` and `src/layouts/CVLayout.astro`, delete `<link rel="stylesheet" href="/assets/css/main.css?v=1" />` and add `import "../styles/main.css";` in the frontmatter; verify no file under `src/` references `/assets/css/main.css` anymore (grep returns zero matches)

## 2. Build and served-asset verification

- [x] 2.1 Run `npm run build` and verify it exits 0 with the 15 static routes; confirm `dist/` contains no verbatim `public` copy of `main.css` (no `dist/assets/css/main.css`)
- [x] 2.2 Fetch the home page from `npm run preview`, confirm the HTML links a bundled CSS asset under `/_astro/`, and confirm that CSS contains compiled Tailwind utilities (`.flex`, dark-variant selectors) plus the custom classes `card-proyecto`, `navlink`, `pill--primary` and the Onest font-face from fonts.css

## Workflow follow-up

- Archive the change after styles are verified in build output.
