# Changelog

All notable changes to the Bäckeli theme are recorded here, newest first.

## 2026-06-29 — Custom images for the collection list

Each collection tile on the homepage is now an individual **Collection card** block with its own **Custom image** picker and collection link, editable live in the theme editor. A custom image overrides the collection's default image; when left blank it falls back to the collection image → first product image → placeholder. Horizon's native `collection-list` section is left untouched.

| File | Change |
| --- | --- |
| [sections/collection-list-custom.liquid](sections/collection-list-custom.liquid) | **New section** — responsive CSS-grid of `collection-card` blocks, with heading/subheading, columns (desktop + mobile), gap, width, background, and padding settings. |
| [blocks/collection-card.liquid](blocks/collection-card.liquid) | Added a **Custom image** image picker next to the collection picker and forwarded it to the image sub-block. |
| [blocks/_collection-card-image.liquid](blocks/_collection-card-image.liquid) | Passes the custom image override through to the `resource-image` snippet. |
| [snippets/resource-image.liquid](snippets/resource-image.liquid) | Prefers the custom image when provided, otherwise uses the existing collection-image fallback chain. |
| [templates/index.json](templates/index.json) | Repointed the homepage collection row to the new section, ported the "Bäckeli moments" heading, and seeded 3 starter tiles. |
