# Changelog

All notable changes to the Bäckeli theme are recorded here, newest first.

## 2026-06-29 — Collection grid: heading & subheading colors

Added **Heading color** and **Subheading color** pickers to the collection grid section. Both default to blank (inherit the section's text color) so existing sections are unaffected. Card titles already have their own **Text color** setting via the Collection title block, so per-card text color is unchanged.

| File | Change |
| --- | --- |
| [sections/collection-list-custom.liquid](sections/collection-list-custom.liquid) | Added `heading_color` / `subheading_color` settings, applied as inline `color` only when set. |

## 2026-06-29 — New section: Come visit us (with map)

Added a two-column **Come visit us** contact section — heading, subheading, address/phone/email rows (with icons), Get directions + Call buttons (brand styled), and Instagram/Facebook links on one side; an embedded Google map on the other. The map needs **no API key**: it's generated from the address via Google's `output=embed` endpoint, with optional zoom, height, left/right placement, and a custom-embed-URL override. Phone/email auto-link (`tel:` / `mailto:`); the Call button falls back to a `tel:` link from the phone number.

| File | Change |
| --- | --- |
| [sections/come-visit-us.liquid](sections/come-visit-us.liquid) | **New section.** Adds from the editor's **Contact** category; reuses the theme's `.button` / `.button-secondary` styles and `instagram`/`facebook` icons, inlines pin/phone/mail icons. Includes heading/subheading sizes + colors, side margin, background, and padding. |

## 2026-06-29 — Text block: mobile font size

Added a **Mobile size** option to the **Text** block (used for the hero heading and subheading, among others). When set, it overrides the font size on phones (≤749px) so large hero headings like “a Taste of Germany” can be sized down to fit on one line; left on “Same as desktop” it changes nothing. Only shows when the block uses the **Custom** type preset.

| File | Change |
| --- | --- |
| [blocks/text.liquid](blocks/text.liquid) | New `font_size_mobile` select (10–72px, default “Same as desktop”). |
| [snippets/text.liquid](snippets/text.liquid) | Emits `--font-size-mobile` + a `custom-font-size-mobile` class, with a ≤749px rule (specificity-bumped to beat base.css) that applies it. |

## 2026-06-29 — New section: Media grid

Added a standalone **Media grid** section — a heading/subheading plus a responsive grid of plain image tiles, each with its own image, aspect ratio, caption, and optional link. Unlike the collection grid, tiles are simple `media` blocks edited directly in the theme editor (no collection / private-static-block plumbing), so images and captions behave predictably. Carries over the same niceties: header + caption color pickers, 7 aspect-ratio options, desktop side margin, columns/gap/width/background/padding.

| File | Change |
| --- | --- |
| [sections/media-grid.liquid](sections/media-grid.liquid) | **New section.** Adds from the editor's **Image** category as “Media grid”; ships a 3-tile preset matching the "Bäckeli moments" layout. |

### Update — heading & subheading font size

Added **Heading size** (20–96px) and **Subheading size** (12–40px) range settings to the Media grid header. Sizes apply on desktop and scale down on mobile (heading ×0.7, subheading ×0.85) so large values don't overflow on phones.

## 2026-06-29 — Collection grid: editable aspect ratio per card

The **Aspect ratio** control now lives on the **Collection card** block itself (next to the Custom image picker), so it's editable in the theme editor. Previously it sat on the private, static `_collection-card-image` sub-block, whose settings aren't reachable in the editor — so the ratio couldn't actually be changed. The parent's choice is forwarded down to the image and wins over the sub-block's value.

| File | Change |
| --- | --- |
| [blocks/collection-card.liquid](blocks/collection-card.liquid) | Added an **Aspect ratio** select (Auto / 9:16 / 5:7 / 4:5 / 1:1 / 7:5 / 16:9, default 4:5) and forwards it to the image as `ratio_override`. |
| [blocks/_collection-card-image.liquid](blocks/_collection-card-image.liquid) | Accepts `ratio_override` and passes it through to `resource-image`. |
| [snippets/resource-image.liquid](snippets/resource-image.liquid) | New optional `image_ratio` param overrides the block's own setting; falls back to it when absent. |

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
