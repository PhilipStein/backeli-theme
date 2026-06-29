# Changelog

All notable changes to the Bäckeli theme are recorded here, newest first.

## 2026-06-29 — Collection grid: heading & subheading colors

Added **Heading color** and **Subheading color** pickers to the collection grid section. Both default to blank (inherit the section's text color) so existing sections are unaffected. Card titles already have their own **Text color** setting via the Collection title block, so per-card text color is unchanged.

| File | Change |
| --- | --- |
| [sections/collection-list-custom.liquid](sections/collection-list-custom.liquid) | Added `heading_color` / `subheading_color` settings, applied as inline `color` only when set. |

## 2026-06-29 — Collection grid: more aspect ratios + desktop side margin

Each collection card can now use more **image aspect ratios**, and the collection grid section can be inset from the left and right edges on desktop.

| File | Change |
| --- | --- |
| [blocks/_collection-card-image.liquid](blocks/_collection-card-image.liquid) | Added aspect-ratio options **Tall (9:16)**, **Portrait (5:7)**, and **Landscape (7:5)** alongside the existing Auto / Portrait (4:5) / Square / Landscape (16:9). |
| [snippets/resource-image.liquid](snippets/resource-image.liquid) | Maps the new ratio values (`tall-9-16`, `tall-5-7`, `wide-7-5`) to their `aspect-ratio` CSS. |
| [sections/collection-list-custom.liquid](sections/collection-list-custom.liquid) | Added a **Side margin (desktop)** range setting (0–200px) that adds inline padding to the left and right of the section on screens ≥750px. |

## 2026-06-29 — Brand fonts (Fredoka + Nunito), self-hosted

Added the Fredoka (headings) and Nunito (body) brand fonts as **self-hosted variable** `woff2` files and activated the brand style mapping so they apply across the theme. Served from Shopify's CDN rather than Google Fonts — faster, no third-party request, and `font-display: swap` to avoid invisible text while loading.

| File | Change |
| --- | --- |
| `assets/fredoka.woff2`, `assets/nunito.woff2`, `assets/nunito-italic.woff2` | Variable font files covering the full weight range (Fredoka 300–700, Nunito 200–1000 + italics), latin subset (covers German `ä ö ü ß €`). |
| [snippets/brand-styles.liquid](snippets/brand-styles.liquid) | Added `@font-face` rules (self-hosted via `asset_url`) and maps Fredoka/Nunito onto Horizon's font variables, plus heading letter-spacing and button tracking. |
| [layout/theme.liquid](layout/theme.liquid) | Renders `brand-styles` after `color-palette` (it was previously not rendered anywhere). |

## 2026-06-29 — Custom images for the collection list

Each collection tile on the homepage is now an individual **Collection card** block with its own **Custom image** picker and collection link, editable live in the theme editor. A custom image overrides the collection's default image; when left blank it falls back to the collection image → first product image → placeholder. Horizon's native `collection-list` section is left untouched.

| File | Change |
| --- | --- |
| [sections/collection-list-custom.liquid](sections/collection-list-custom.liquid) | **New section** — responsive CSS-grid of `collection-card` blocks, with heading/subheading, columns (desktop + mobile), gap, width, background, and padding settings. |
| [blocks/collection-card.liquid](blocks/collection-card.liquid) | Added a **Custom image** image picker next to the collection picker and forwarded it to the image sub-block. |
| [blocks/_collection-card-image.liquid](blocks/_collection-card-image.liquid) | Passes the custom image override through to the `resource-image` snippet. |
| [snippets/resource-image.liquid](snippets/resource-image.liquid) | Prefers the custom image when provided, otherwise uses the existing collection-image fallback chain. |
| [templates/index.json](templates/index.json) | Repointed the homepage collection row to the new section, ported the "Bäckeli moments" heading, and seeded 3 starter tiles. |
