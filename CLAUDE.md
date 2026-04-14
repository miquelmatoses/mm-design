# mm-design

## Purpose

Centralized design system extracted from the **cercol.team** visual identity. This repo is the single source of truth for design tokens, reusable components, and documentation shared across all personal and professional projects by Miquel Matoses.

Every project (cercol.team, topquaranta.cat, portfolio, etc.) imports from this repo rather than defining its own colors, typography, or spacing. Changes propagate from here.

## Architecture

```
mm-design/
  tokens/           # CSS files defining custom properties (colors, typography, spacing, etc.)
  components/       # Standalone HTML+CSS components (buttons, cards, nav, etc.)
  docs/             # Usage guides, examples, changelog
  index.html        # Live preview page — renders all tokens and components
  CLAUDE.md         # This file
```

- **tokens/** — One CSS file per category (e.g. `colors.css`, `typography.css`, `spacing.css`). Each file only contains `:root` declarations with `--mm-` prefixed custom properties.
- **components/** — Each component is a folder with its own `.css` file and an optional `.html` snippet showing usage. Components consume tokens exclusively via `var(--mm-*)`.
- **docs/** — Markdown files explaining design decisions, how to consume the system, and a changelog.
- **index.html** — A plain HTML page that imports all token and component CSS files and renders a visual reference. Open it directly in a browser (no build step).

## Token naming convention

All CSS custom properties follow:

```
--mm-[category]-[name]
```

Examples:

```css
--mm-color-primary
--mm-color-surface
--mm-font-heading
--mm-font-body
--mm-space-sm
--mm-space-md
--mm-radius-sm
--mm-shadow-card
```

Categories include: `color`, `font`, `space`, `radius`, `shadow`, `size`, `weight`, `line`, `letter`.

Never use raw values in components — always reference a token.

## Tech constraints

- **Vanilla HTML + CSS only.** No JavaScript logic, no preprocessors, no build step.
- The system must be consumable by importing CSS files directly. No compilation required to use it.
- **Importable in:**
  - **React (Vite)** — import the CSS files in `main.tsx` or individual components.
  - **Django / Wagtail** — load via `<link>` in base templates or `{% static %}` tags.
  - **Plain HTML / GitHub Pages** — `<link rel="stylesheet" href="...">` with relative or CDN paths.
- Files must work when served from a local file path, a dev server, or a static host.
- No `@import` chains that break without a bundler. Each CSS file is self-contained (tokens files declare `:root` vars; component files consume them).

## Workflow

### Adding a new token

1. Open (or create) the appropriate file in `tokens/` (e.g. `colors.css`).
2. Add the custom property under `:root` using the `--mm-[category]-[name]` convention.
3. Update `index.html` to display the new token in the preview.
4. Commit with a message like `tokens: add --mm-color-accent`.

### Adding a new component

1. Create a folder in `components/` named after the component (e.g. `components/button/`).
2. Add a `button.css` that styles the component using only `var(--mm-*)` tokens.
3. Add a `button.html` snippet showing example markup.
4. Import the CSS in `index.html` and add a section rendering the example.
5. Commit with a message like `components: add button`.

### Updating the live preview

1. Open `index.html` in a browser.
2. The page pulls in all token and component CSS files. No build needed — just refresh.
3. To add a new section, edit `index.html` directly.

## Icons

The `icons/` directory contains 37 SVG icons across 4 families:

- **moon/** (4 icons, 32×32) — phase icons: new-moon, first-quarter, full-moon, last-quarter
- **dimension/** (5 icons, 24×24) — Big Five domain symbols: presence, bond, vision, depth, discipline
- **animals/** (12 icons) — role animal silhouettes: R01 dolphin through R12 badger
- **ui/** (16 icons, 24×24) — functional UI icons: arrows, check, close, share, user, globe, etc.
- **react/MoonIcons.jsx** — React component exports for all icons, including `RoleIcon` and `DimensionIcon` wrappers

### Icon rules

- All consuming projects **must** source icons from this repo. Never create project-local icon files.
- If a project needs a new icon, it **must** be added here first:
  1. Add the SVG file to the appropriate family folder in `icons/`
  2. Add the React export to `icons/react/MoonIcons.jsx`
  3. Update `index.html` preview if relevant
  4. Commit, then import in the consuming project
- No external icon libraries (Lucide, Heroicons, Font Awesome, etc.) in any consuming project.
- SVG icons use `currentColor` — color is set by the parent element.

## JavaScript token exports

`tokens/index.js` exports all design tokens as JavaScript objects for React/Vite consumers:

```js
import { colors, fonts, spacing, ROLE_COLORS, DOMAIN_COLORS } from 'mm-design/tokens/index.js'
```

This file is auto-derived from the JSON token files. Keep both in sync.

## Out of scope

- No JavaScript logic beyond token exports and icon components (interactions, state, event handling belong in consuming projects).
- No third-party dependencies — zero npm packages, zero CDN libs.

## Cross-repo enforcement rules

Every project that consumes mm-design **must** follow these rules (enforced via each project's CLAUDE.md):

1. **Tokens**: All colors, fonts, spacing, and shadows come from mm-design. Never hardcode hex values.
2. **Fonts**: Playfair Display (headings), Roboto (body), JetBrains Mono (code). No other fonts.
3. **Icons**: All icons come from `mm-design/icons/`. If a new icon is needed, add it here first (SVG + React export), then import it in the consuming project.
4. **Components**: Use mm-design CSS component classes (`.mm-btn`, `.mm-card`, etc.) where applicable.
5. **README badges**: All shields.io badge hex colors must use the mm-design brand palette (see `tokens/badge-colors.md`):
   - Red: `cf3339` · Blue: `0047ba` · Yellow: `f1c22f` · Green: `427c42` · Black: `111111`
6. **No parallel design systems**: Never create local token files, color constants, or icon collections that duplicate mm-design.

## Consuming projects

| Project | Stack | How it imports mm-design |
|---|---|---|
| **cercol.team** | React / Vite | CSS files imported in `main.tsx` or via Vite's CSS handling |
| **topquaranta.cat** | Django / Wagtail | Loaded via `<link>` in base template or `{% static %}` |
| **portfolio** | GitHub Pages (plain HTML) | `<link rel="stylesheet">` pointing to raw or hosted CSS files |
