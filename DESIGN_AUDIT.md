# Design Audit — cercol.team

Extracted from the cercol.team codebase (`src/design/tokens.js`, `src/index.css`,
`src/App.css`, `src/components/`, `src/pages/`). Source of truth for migrating values
into the mm-design token system.

---

## 1. CSS Custom Properties (globally defined)

The project defines **no `:root`-level CSS custom properties**. All design tokens
live in `src/design/tokens.js` as JavaScript exports consumed by React components.

Seven CSS variables are referenced in `src/App.css` but **never defined** in source
(likely remnants from a Vite scaffold):

| Variable | Used for |
|---|---|
| `--accent` | Counter text color, focus outline |
| `--accent-bg` | Counter background |
| `--accent-border` | Counter hover border |
| `--border` | Section dividers |
| `--text-h` | Link heading color |
| `--social-bg` | Social link background |
| `--shadow` | Hover box-shadow |

These are orphaned and unused by the live product.

---

## 2. Color palette

### 2.1 Brand palette

| Name | Hex | Usage |
|---|---|---|
| Red | `#cf3339` | Primary CTA, error state, role R01 |
| Blue | `#0047ba` | Buttons, links, header, role arc bar |
| Yellow | `#f1c22f` | Warning state, discipline dimension |
| Green | `#427c42` | Success state, role R05, bond dimension |
| White | `#ffffff` | Background, surface |
| Black | `#111111` | Body text, depth dimension |

### 2.2 Semantic aliases

| Token | Hex | Role |
|---|---|---|
| `primary` | `#cf3339` | Primary CTA (red) |
| `primaryDark` | `#a8262b` | Darker red (hover/active) |
| `background` | `#ffffff` | Page background |
| `surface` | `#ffffff` | Card/container surface |
| `border` | `#d4d4d4` | Default border |
| `textPrimary` | `#111111` | Body text |
| `textMuted` | `#666666` | Secondary/muted text |
| `success` | `#427c42` | Success semantic |
| `warning` | `#f1c22f` | Warning semantic |
| `error` | `#cf3339` | Error semantic |

### 2.3 Report UI colors

| Token | Hex | Role |
|---|---|---|
| `arcBar` | `#0047ba` | Arc role bar fill |
| `arcLabel` | `#0047ba` | Arc role label text |
| `selfBar` | `#9ca3af` | Self-report bar (gray-400) |
| `trackBg` | `#f3f4f6` | Progress bar background (gray-100) |

### 2.4 Big Five / radar chart colors

| Token | Hex | Tailwind equivalent |
|---|---|---|
| `openness` | `#0047ba` | — |
| `conscientiousness` | `#f1c22f` | — |
| `extraversion` | `#cf3339` | — |
| `agreeableness` | `#427c42` | — |
| `neuroticism` | `#111111` | — |

### 2.5 Domain colors (bar fills in reports)

| Domain | Hex | Tailwind class |
|---|---|---|
| Presence | `#fbbf24` | `bg-amber-400` / `text-amber-400` |
| Bond | `#10b981` | `bg-emerald-500` / `text-emerald-500` |
| Vision | `#427c42` | `bg-[#427c42]` / `text-[#427c42]` |
| Discipline | `#2563eb` | `bg-blue-600` / `text-blue-600` |
| Depth | `#ef4444` | `bg-red-500` / `text-red-500` |

### 2.6 Balance status colors (pills)

| State | Background | Text |
|---|---|---|
| Balanced / Good | `#f0fdf4` | `#166534` |
| Tilted High/Low | `#fef9c3` | `#854d0e` |
| Strongly High/Low / Caution | `#fee2e2` | `#991b1b` |

### 2.7 Role colors (R01-R12)

12 distinct hues, 30 degrees apart. Brand anchors: R01 = red, R05 = green.

| Role | Name | Hex | Hue |
|---|---|---|---|
| R01 | Dolphin | `#cf3339` | Red (brand) |
| R02 | Wolf | `#d46010` | Orange |
| R03 | Elephant | `#c08800` | Amber |
| R04 | Owl | `#6a8800` | Olive |
| R05 | Eagle | `#427c42` | Green (brand) |
| R06 | Falcon | `#1a8c60` | Emerald |
| R07 | Octopus | `#0d8888` | Teal |
| R08 | Tortoise | `#1a68b0` | Cerulean |
| R09 | Bee | `#3355c8` | Cobalt |
| R10 | Bear | `#6630a8` | Indigo |
| R11 | Fox | `#a030a0` | Violet |
| R12 | Badger | `#b03070` | Crimson |

### 2.8 Interactive / UI accent colors (used inline in components)

| Hex | Usage |
|---|---|
| `#e8eef8` | Light blue hover background (LikertScale) |
| `#99b3e0` | Focus ring (medium blue) |
| `#003090` | Hover text (dark blue) |

### 2.9 Neutral gray palette (Tailwind defaults in use)

| Tailwind | Hex | Usage |
|---|---|---|
| `gray-50` | `#f9fafb` | Hover menu backgrounds |
| `gray-100` | `#f3f4f6` | Section backgrounds, badge default bg |
| `gray-200` | `#e5e7eb` | Card default border, dividers |
| `gray-300` | `#d1d5db` | Subtle elements |
| `gray-400` | `#9ca3af` | Muted text, placeholder |
| `gray-500` | `#6b7280` | Secondary text |
| `gray-600` | `#4b5563` | Readable body text |
| `gray-700` | `#374151` | Default body text, badge default text |
| `gray-800` | `#1f2937` | Dark text |
| `gray-900` | `#111827` | Very dark text, print bg |

### 2.10 RGBA / opacity values

| Value | Usage |
|---|---|
| `rgba(255,255,255,0.5)` | Semi-transparent white text (hero) |
| `rgba(255,255,255,0.7)` | Nav inactive text (`text-white/70`) |
| `rgba(0,0,0,0.08)` | Subtle dark overlay |
| `rgba(0,0,0,0.12)` | Subtle dark overlay |
| Hex + `22` suffix | 13% opacity tint for facet bar backgrounds |
| Hex + `18` suffix | 9% opacity tint for highlights |
| `opacity: 0.85` | Witness marker |
| `opacity: 0.55` | Muted role icon |
| `opacity: 0.38` | Faded role icon |

---

## 3. Typography

### 3.1 Font families

| Token | Stack | Weight imported | Usage |
|---|---|---|---|
| `display` | `"Playfair Display", Georgia, serif` | 400, 700 | h1, h2, h3 |
| `sans` | `"Roboto", system-ui, sans-serif` | 400, 500, 700 | Body, UI, buttons |
| `mono` | `"JetBrains Mono", monospace` | — | Code, tables |

Loaded via Google Fonts in `index.css`:
```
https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=Roboto:wght@400;500;700&display=swap
```

### 3.2 Font sizes in use

| Tailwind class | Approximate px | Where used |
|---|---|---|
| `text-xs` | 12px | Badges, labels, nav links, section labels |
| `text-sm` | 14px | Buttons (md/lg), body paragraphs, descriptions |
| `text-base` | 16px | Standard body |
| `text-lg` | 18px | Section headings, question text |
| `text-xl` | 20px | Question text (sm breakpoint) |
| `text-2xl` | 24px | Card titles (HomePage) |
| `text-3xl` | 30px | Page titles |
| `text-5xl` | 48px | Role name (mobile) |
| `text-6xl` | 60px | Role name (desktop) |

Inline sizes: `11px`, `12px`, `13px` (RadarChart labels/tooltips only).

### 3.3 Font weights in use

| Tailwind | Value | Usage |
|---|---|---|
| `font-normal` | 400 | Body text, descriptions |
| `font-medium` | 500 | Nav links, form labels |
| `font-semibold` | 600 | Buttons, badges, section labels, bar labels |
| `font-bold` | 700 | Headings, card titles, role names |

### 3.4 Line heights in use

| Tailwind | Multiplier | Usage |
|---|---|---|
| `leading-none` | 1.0 | Icon containers |
| `leading-tight` | 1.25 | Role name headings |
| `leading-snug` | 1.375 | Question text, anchor labels |
| `leading-relaxed` | 1.625 | Descriptions, body paragraphs |

### 3.5 Letter spacing in use

| Tailwind | Value | Usage |
|---|---|---|
| `tracking-wide` | 0.025em | Standard wide text |
| `tracking-widest` | 0.1em | Section labels (uppercase eyebrows) |

### 3.6 Text utilities

- `uppercase` — section labels, arc badges, domain labels
- `italic` — question card text
- `tabular-nums` — probability percentages, dimension scores

---

## 4. Spacing patterns

### 4.1 Spacing scale (recurring values, 4px base)

| Step | Rem | Px | Tailwind | Usage examples |
|---|---|---|---|---|
| 0.5 | 0.125 | 2px | `gap-0.5` | Tight icon gaps |
| 1 | 0.25 | 4px | `p-1`, `gap-1` | Small padding, tiny margins |
| 1.5 | 0.375 | 6px | `p-1.5`, `gap-1.5` | Icon button padding |
| 2 | 0.5 | 8px | `gap-2`, `mb-2` | Standard small gap |
| 2.5 | 0.625 | 10px | `px-2.5`, `py-2.5` | Badge/button padding |
| 3 | 0.75 | 12px | `px-3`, `gap-3` | Button sm padding, menu items |
| 4 | 1.0 | 16px | `gap-4`, `mb-4` | Card sections, icon spacing |
| 5 | 1.25 | 20px | `p-5`, `px-5` | Card default padding |
| 6 | 1.5 | 24px | `p-6`, `gap-6` | Large card padding, grid gaps |
| 8 | 2.0 | 32px | `p-8`, `gap-8` | Page-level horizontal padding |

### 4.2 Max-width / containers

| Value | Tailwind | Usage |
|---|---|---|
| 720px | — (tokens.js `pageMax`) | Doc-page content width |
| 896px (56rem) | `max-w-4xl` | Layout content wrapper |
| — | `max-w-screen-xl` | HomePage instrument grid |

### 4.3 Border radius

| Value | Tailwind | Usage |
|---|---|---|
| 4px | `rounded` | Default (global for buttons/inputs/cards) |
| 9999px | `rounded-full` | Progress bars, avatars, likert buttons |
| 2px | `rounded-sm` | Small elements |
| 12px | — (inline) | Radar chart tooltip |

### 4.4 Box shadows

| Tailwind | Usage |
|---|---|
| `shadow-sm` | Cards, buttons |
| `shadow-md` | Card hover states |
| `shadow-lg` | Dropdown menus |

### 4.5 Z-index layers

| Value | Tailwind | Usage |
|---|---|---|
| 0 | — | Hero base layer |
| 1 | — | Hero framework layer |
| 50 | `z-50` | Cookie banner, dropdown menus, feedback button |

---

## 5. Responsive breakpoints

Standard Tailwind defaults (no customization):

| Prefix | Min-width | Usage |
|---|---|---|
| (none) | 0px | Mobile-first base |
| `sm:` | 640px | Card padding, likert layout switch |
| `md:` | 768px | Nav visibility, 2-col grids |
| `lg:` | 1024px | Page padding, wider layouts |
| `xl:` | 1280px | 4-col grid (HomePage instruments) |

One custom breakpoint in `App.css`: `@media (max-width: 1024px)`.

---

## 6. Tailwind custom configuration

**No `tailwind.config.js` exists.** The project uses Tailwind CSS v4.2.2 via
`@tailwindcss/vite` with zero theme extensions. All custom values are applied
through arbitrary value syntax (`text-[#0047ba]`, `bg-[#427c42]`) or the JS
tokens file.

No plugins. No PostCSS config file.

---

## 7. Reusable UI components

### Button

| Prop | Values | Default |
|---|---|---|
| `variant` | `primary` / `secondary` / `ghost` | `primary` |
| `size` | `sm` / `md` / `lg` | `md` |

| Variant | Fill | Text | Border | Hover |
|---|---|---|---|---|
| `primary` | `#0047ba` | white | none | `opacity: 0.9` |
| `secondary` | white | `#0047ba` | `1px #0047ba` | Fill blue, text white |
| `ghost` | none | `#0047ba` | none | Underline |

Sizes: `sm` = `text-xs px-3 py-1.5`, `md` = `text-sm px-5 py-2.5`, `lg` = `text-sm px-6 py-3`.
All: `font-semibold`, `rounded` (4px), `transition-colors`, `disabled:opacity-50`.

### Card

| Prop | Values | Default |
|---|---|---|
| `accent` | `none` / `red` / `green` / `yellow` / `blue` | `none` |

- Default: `bg-white border border-gray-200 rounded`
- Accented: `bg-white rounded` + 3px left border in accent color, no other border

Accent colors: red `#cf3339`, green `#427c42`, yellow `#f1c22f`, blue `#0047ba`.

### Badge

| Prop | Values | Default |
|---|---|---|
| `variant` | `default` / `beta` / `paid` / `free` | `default` |

| Variant | Background | Text |
|---|---|---|
| `default` | `gray-100` | `gray-700` |
| `beta` | `#f1c22f` | `#111111` |
| `paid` | `#0047ba` | white |
| `free` | `#427c42` | white |

All: `text-xs font-semibold px-2.5 py-1 rounded`.

### SectionLabel

| Prop | Values | Default |
|---|---|---|
| `color` | `blue` / `red` / `green` / `amber` / `gray` | `gray` |

| Color | Tailwind class |
|---|---|
| `blue` | `text-[#0047ba]` |
| `red` | `text-[#cf3339]` |
| `green` | `text-[#427c42]` |
| `amber` | `text-amber-500` |
| `gray` | `text-gray-400` |

All: `text-xs font-semibold uppercase tracking-widest`.

### Other reusable components

| Component | Purpose | Key visual traits |
|---|---|---|
| **LikertScale** | 1-7 rating buttons | Vertical on mobile, horizontal on desktop. Selected: blue fill. Hover: `border-[#0047ba] bg-[#e8eef8]` |
| **QuestionCard** | Question wrapper with LikertScale | White bg, `border border-gray-200`, `p-6 sm:p-8 rounded` |
| **ProgressBar** | Animated fill bar | `h-2 rounded-full`, track `bg-gray-200`, fill from tokens, `transition-all duration-300` |
| **LanguageToggle** | Globe + dropdown | `hover:bg-white/10 transition-colors` |
| **AccountButton** | Avatar + dropdown menu | `w-7 h-7 rounded-full`, dropdown `z-50 w-44 shadow-lg` |
| **CookieBanner** | Fixed bottom banner | `fixed bottom-0 z-50`, bg `#111111` |
| **FeedbackButton** | Floating action button | `fixed bottom-5 right-5 z-50`, `shadow-sm hover:shadow-md` |
| **FacetAccordion** | Collapsible domain card | Chevron rotates 90deg on expand, `transition-transform duration-200` |
| **ConvergenceMeter** | Convergence progress bar | `transition-all duration-700`. Colors: emerald (60%+), amber (30-60%), red (<30%) |
| **DimensionRow** | Domain score + bar | Standard and compact modes. Bar `transition-all duration-500` |
| **RoleCard** | Large role display | `text-5xl sm:text-6xl font-bold`, red accent card |
| **RoleProbabilityBars** | Ranked bars for 12 roles | Row opacity: 1.0 (primary), 0.7 (arc), 0.45 (others). `transition-all duration-500` |
| **RadarChart** | Organic radar shape | Recharts-based. Catmull-Rom to cubic Bezier (tension 0.4). Radial gradient: red `#cf3339` at opacity 0.18 (center) to 0.58 (edge). No render animation. |

---

## 8. Animation and transition patterns

### Transition classes in use

| Pattern | Duration | Usage |
|---|---|---|
| `transition-colors` | 150ms (default) | Buttons, nav links, menu items, banner links |
| `transition-opacity` | 150ms (default) | Avatar hover, feedback button |
| `transition-all` | 150ms (default) | LikertScale, feedback button |
| `transition-all duration-300` | 300ms | ProgressBar fill |
| `transition-all duration-500` | 500ms | Domain bars, facet bars, role probability bars |
| `transition-all duration-700` | 700ms | ConvergenceMeter |
| `transition-transform duration-200` | 200ms | Accordion chevron rotation |

### Hover/focus patterns

| Element | Hover | Focus | Disabled |
|---|---|---|---|
| Button primary | `opacity: 0.9` | `outline: 2px offset-2` | `opacity: 0.5` |
| Button secondary | Fill blue + white text | — | `opacity: 0.5` |
| Button ghost | Underline | — | `opacity: 0.5` |
| LikertScale | `border-[#0047ba] bg-[#e8eef8]` | — | — |
| Nav link (inactive) | `text-white bg-white/10` | — | — |
| Nav link (active) | — (already `text-white bg-white/20`) | — | — |
| Menu items | `bg-gray-50` | — | — |
| Card (feedback) | `shadow-md` | — | — |

### CSS transitions (App.css)

- `transition: border-color 0.3s` — counter hover
- `transition: box-shadow 0.3s` — social link hover

### Keyframes / animations

None. The project uses exclusively CSS transitions. No `@keyframes`, no
Framer Motion, no animation libraries.

---

## 9. Print styles

Defined in `src/index.css` for the Last Quarter report page:

- Page size: A4 landscape, 1cm margins
- Body font: 11px
- Hidden: header, nav, fixed overlays, shadows
- Top grid: `40% 30% 30%` three-column
- Bottom grid: `50% 50%` two-column
- All facet panels forced open
- `print-color-adjust: exact` for background colors

---

## 10. Layout patterns

### Header

`h-16` (64px), `flex items-center gap-6 px-6 lg:px-12`, brand blue background.

### Content wrapper

`max-w-4xl mx-auto` (896px centered).

### Common grids

| Pattern | Tailwind |
|---|---|
| 2-col responsive | `grid grid-cols-1 md:grid-cols-2 gap-4` |
| 3-col responsive | `grid grid-cols-1 md:grid-cols-3 gap-4` |
| 2-col facets | `grid grid-cols-1 sm:grid-cols-2 gap-x-6 gap-y-4` |
| 4-col instruments | `grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-4 gap-6` |

---

## 11. Icons

### 11.1 Icon libraries

**None.** No external icon packages (lucide, heroicons, react-icons, phosphor, etc.)
are installed. Every icon is custom-built as an inline SVG React component or an
imported raw SVG file.

### 11.2 Central icon file

All icons live in `src/components/MoonIcons.jsx`. The project convention forbids
inline SVG outside this file. Two wrapper components provide the public API:

- **`RoleIcon({ role, size, className, style })`** — maps `R01`–`R12` to the
  corresponding animal icon. Default size 32px. Returns null for unknown keys.
- **`DimensionIcon({ domain, size, className, style })`** — maps domain keys
  (`presence`, `bond`, `vision`, `depth`, `discipline`) to symbolic icons.
  Default size 24px.

### 11.3 Moon / phase icons

Inline SVG components, stroke-based, `currentColor`, hand-drawn style.

| Export | ViewBox | Default size | Description |
|---|---|---|---|
| `NewMoonIcon` | `0 0 32 32` | 32px | Dark circle with diagonal hatching (unlit face) |
| `FirstQuarterIcon` | `0 0 32 32` | 32px | Right half illuminated, inward terminator curve |
| `FullMoonIcon` | `0 0 32 32` | 32px | Full disk with three crater marks |
| `LastQuarterIcon` | `0 0 32 32` | 32px | Left half illuminated (mirrored first quarter) |

Usage contexts and sizes:

| Location | Icons | Size |
|---|---|---|
| HomePage instrument cards | All four phases | 80px |
| Instrument pages (NewMoon, FirstQuarter, FullMoon) | Matching phase | 36–40px |
| Result pages (NewMoon, FirstQuarter, FullMoon) | Matching phase | 18px |
| InstrumentsPage labels | NewMoon, FirstQuarter, FullMoon | 13px |
| LastQuarterPage header | LastQuarter | 20px |
| WitnessSetupPage | FullMoon | 13px |

### 11.4 Animal role icons (R01-R12)

Stored as SVG files in `src/assets/icons/animals/`, imported via Vite's `?raw`
loader, and rendered through `dangerouslySetInnerHTML` with pre-sanitized content.
Generated by potrace from hand-drawn artwork. All use `fill="currentColor"`.

| File | Role | Animal | Export |
|---|---|---|---|
| `cercol-icon-r01-dolphin.svg` | R01 | Dolphin | `DolphinIcon` |
| `cercol-icon-r02-wolf.svg` | R02 | Wolf | `WolfIcon` |
| `cercol-icon-r03-elephant.svg` | R03 | Elephant | `ElephantIcon` |
| `cercol-icon-r04-owl.svg` | R04 | Owl | `OwlIcon` |
| `cercol-icon-r05-eagle.svg` | R05 | Eagle | `EagleIcon` |
| `cercol-icon-r06-falcon.svg` | R06 | Falcon | `FalconIcon` |
| `cercol-icon-r07-octopus.svg` | R07 | Octopus | `OctopusIcon` |
| `cercol-icon-r08-tortoise.svg` | R08 | Tortoise | `TortoiseIcon` |
| `cercol-icon-r09-bee.svg` | R09 | Bee | `BeeIcon` |
| `cercol-icon-r10-bear.svg` | R10 | Bear | `BearIcon` |
| `cercol-icon-r11-fox.svg` | R11 | Fox | `FoxIcon` |
| `cercol-icon-r12-badger.svg` | R12 | Badger | `BadgerIcon` |

SVG import pipeline: raw string → `prepareAnimalSvg()` extracts `viewBox` and
inner `<g>` content at module load → `AnimalSvg` wrapper renders with
`dangerouslySetInnerHTML`.

Usage contexts and sizes:

| Location | Size | Notes |
|---|---|---|
| RoleResult / RoleCard (report) | 128px | Large display, `color: colors.red` |
| AccountButton (header avatar) | 26px | White on blue header |
| RoleProbabilityBars | 16px | Inline next to bar |
| HomePage instrument cards | varies | Opacity 0.38 (decorative) |

### 11.5 Dimension icons

Inline SVG components, stroke-based, 24×24 viewBox.

| Export | Domain | Symbol | Color class |
|---|---|---|---|
| `PresenceIcon` | Presence (Extraversion) | Radiating lines | `text-amber-400` |
| `BondIcon` | Bond (Agreeableness) | Two interlocking circles | `text-emerald-500` |
| `VisionIcon` | Vision (Openness) | Eye with iris/pupil | `text-[#427c42]` |
| `DepthIcon` | Depth (Neuroticism) | Three descending wave arcs | `text-red-500` |
| `DisciplineIcon` | Discipline (Conscientiousness) | Three concentric circles | `text-blue-600` |

Usage: DimensionRow (11–14px), instrument pages (16px), FullMoonPage (36px),
MyResultsPage (13px), AboutPage, SciencePage.

### 11.6 Functional / UI icons

All inline SVG in `MoonIcons.jsx`, stroke-based, `currentColor`.

| Export | ViewBox | Default size | Purpose | Used in |
|---|---|---|---|---|
| `ArrowLeftIcon` | 24×24 | 24px | Back navigation | NewMoon/FirstQuarter/FullMoonPage |
| `ArrowRightIcon` | 24×24 | 24px | Forward navigation | Instrument pages, HomePage, RolesPage, AboutPage |
| `CheckIcon` | 32×32 | 32px | Completion | WitnessPage, WitnessSetupPage |
| `XIcon` | 24×24 | 24px | Negative / worst fit | WitnessPage |
| `ChevronRightIcon` | 24×24 | 24px | Expand / row indicator | FacetAccordion, LastQuarterPage, MyResultsPage |
| `ShareIcon` | 24×24 | 24px | Share / copy | FirstQuarter/FullMoonResultsPage |
| `UserIcon` | 24×24 | 24px | Account / profile | AccountButton |
| `GlobeIcon` | 24×24 | 24px | Language toggle | LanguageToggle |
| `KeyboardIcon` | 24×24 | 24px | Keyboard hints | QuestionCard |
| `InfoCircleIcon` | 24×24 | 24px | Information | WitnessPage |
| `BlindSpotsIcon` | 24×24 | 24px | Self vs witness gap | FullMoonResultsPage |
| `HamburgerIcon` | 20×20 | 20px | Mobile menu | Layout |
| `CloseIcon` | 20×20 | 20px | Dismiss | Layout, WitnessSetupPage |
| `ExternalLinkIcon` | 14×14 | 14px | External link | SciencePage |
| `InfoIcon` | 18×18 | 18px | Small info hint | Various |
| `TranslationIcon` | 13×13 | 13px | Translation feedback | FeedbackButton |

### 11.7 Brand logo

`CercolLogo` — standalone component in `src/components/CercolLogo.jsx`.
Large SVG (viewBox `0 0 1122.52 470.92`), `fill="currentColor"`, used in
Layout header. Supports `aria-label`, `className`, `style`.

### 11.8 Other inline SVG

- **FaqPage.jsx** — single chevron (`viewBox 0 0 24 24`, path `m6 9 6 6 6-6`),
  rotates 180deg on accordion open via `group-open:rotate-180`.

### 11.9 Icon sizing conventions

| Context | Size range | Default |
|---|---|---|
| Moon phases | 13–80px | 32px |
| Role animals | 16–128px | 32px |
| Dimension symbols | 11–36px | 24px |
| Functional UI | 13–24px | 24px |

### 11.10 Assets directory

```
src/assets/
  cercol-logo.svg
  hero.png
  icons/
    animals/
      cercol-icon-r01-dolphin.svg
      cercol-icon-r02-wolf.svg
      cercol-icon-r03-elephant.svg
      cercol-icon-r04-owl.svg
      cercol-icon-r05-eagle.svg
      cercol-icon-r06-falcon.svg
      cercol-icon-r07-octopus.svg
      cercol-icon-r08-tortoise.svg
      cercol-icon-r09-bee.svg
      cercol-icon-r10-bear.svg
      cercol-icon-r11-fox.svg
      cercol-icon-r12-badger.svg
  illustrations/
    (empty)
```
