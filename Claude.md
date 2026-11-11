# Project Blueprint: Rental Property Website

A highly repeatable, single-property rental website layout. The same template should be reusable for any property by swapping out the data file alone.

## Project Structure

```
/
├── Claude.md        # This file: project blueprint and rulebook
├── property.json    # Single source of truth for ALL content and property details
├── index.html       # HTML5 + Tailwind template (layout and design only)
└── assets/          # Optional: local images, icons, etc.
```

---

## Rule 1: Strict Separation of Concerns

- **`property.json` owns all content.** Property name, tagline, descriptions, location, pricing, rates, amenities, room details, house rules, image paths/URLs, alt text, contact info, booking details, SEO metadata, and any other user-facing text live here.
- **`index.html` owns layout and design only.** It defines structure, styling, and interaction. It must not introduce content that isn't sourced from `property.json`.
- No hardcoded property-specific copy, prices, or details in the template beyond what is compiled from `property.json`.
- Keep `property.json` clean and well-organized: logical nested sections (e.g. `meta`, `hero`, `overview`, `pricing`, `amenities`, `gallery`, `rooms`, `location`, `rules`, `contact`), consistent key naming (camelCase), and valid JSON (no comments, no trailing commas).
- Reusing the template for a new property should require changing **only** `property.json` (plus any new image assets).

## Rule 2: Coding Standards

- **HTML:** Clean, semantic HTML5 — use `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<figure>`, `<footer>`, etc. appropriately. One `<h1>` per page with a logical heading hierarchy.
- **CSS:** Modern CSS3 via **Tailwind CSS loaded from CDN**. Prefer Tailwind utility classes; keep any custom CSS minimal and contained in a single `<style>` block or Tailwind config script.
- **JavaScript:** Minimal vanilla JS only, used for interaction (e.g. image carousel, lightbox, modal inquiry/booking forms, mobile nav toggle). Keep it small, readable, and unobtrusive.
- **No heavy frontend frameworks** (no React, Vue, Angular, Svelte, etc.).
- **No build tools** (no npm, bundlers, transpilers, or preprocessors). The site must work by opening/serving `index.html` directly.
- **Accessibility:** Meaningful `alt` text (sourced from `property.json`), labelled form fields, keyboard-operable carousels and modals, sufficient color contrast, and visible focus states.
- **Responsive:** Mobile-first layouts that scale cleanly to tablet and desktop.
- **SEO basics:** Title, meta description, and Open Graph tags populated from `property.json`.

## Rule 3: Modification Guardrails

Whenever a change is requested to text, amenities, prices, or any property details:

1. **Update `property.json` first.** This is always the source of truth.
2. **Then compile the changes into `index.html`** so it accurately reflects the updated data — no omissions, no drift, no invented content.
3. **Verify consistency:** every value shown in `index.html` must match `property.json` exactly (prices, names, counts, lists, links).
4. Never edit content directly in `index.html` without making the corresponding change in `property.json`.

Design/layout-only changes (spacing, colors, component structure, interactions) are made in `index.html` and do not require changes to `property.json`, unless they introduce new content.

---

## Workflow Checklist

- [ ] Content change requested → edit `property.json` → compile into `index.html` → verify values match.
- [ ] Layout change requested → edit `index.html` only → confirm no hardcoded content was introduced.
- [ ] New property → replace `property.json` (and assets) → recompile `index.html`.
