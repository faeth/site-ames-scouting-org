# Ames Scouting — amesscouting.org

Umbrella Scouting site for Ames, Iowa covering Cub Scout packs (Pack 159, Pack 275) and Scouts BSA troops. Built on the [eleventy-excellent](https://github.com/madrilene/eleventy-excellent) starter.

## Stack

- **11ty v3** — static site generator
- **Tailwind v3** — utility classes (via design tokens; no arbitrary values)
- **WebC** — component system for interactive/reusable UI
- **Nunjucks** — templating for layouts and pages
- **PostCSS** — CSS processing (CUBE CSS methodology)
- **Netlify** — deployment (`dist/` published, `.cache/` preserved via plugin)
- **Node >=20**

## Commands

```bash
npm start          # dev server with live reload (http://localhost:8080)
npm run build      # clean + production build → dist/
npm run clean      # remove dist/ and compiled CSS/JS from src/_includes/
npm run favicons   # regenerate favicons from src/assets/svg/misc/logo.svg
npm run colors     # regenerate color tokens
```

## Directory structure

```
src/
  _config/         # 11ty config modules (collections, filters, plugins, shortcodes, setup)
  _data/           # global data
    meta.js          # site name, URL, author, blog, theme — edit here first
    navigation.js    # top/bottom nav arrays
    designTokens/    # JSON design tokens consumed by Tailwind and PostCSS
    personal.yaml    # personal/social links shown in footer
  _includes/       # partials, CSS bundles, JS bundles, WebC components
    css/             # compiled CSS written here by build (gitignored)
    scripts/         # compiled JS written here by build (gitignored)
    partials/        # Nunjucks partials (header, footer, nav, cards, etc.)
    webc/            # WebC components (custom-card, custom-youtube, etc.)
  _layouts/        # base.njk, page.njk, post.njk, tags.njk
  assets/          # static assets copied to dist/
    css/global/      # source CSS (CUBE CSS: base, blocks, compositions, utilities)
    fonts/           # atkinson, redhat (woff2)
    images/          # site images; favicon/ is copied to root
    svg/             # SVGs used via {% svg %} shortcode
    scripts/         # source JS bundles
  pages/           # top-level pages (index, about, join, blog, legal, styleguide)
  posts/           # blog posts (Markdown); posts.json sets shared front matter
  common/          # utility pages: sitemap, feeds, robots.txt, 404, manifest
eleventy.config.js # main 11ty config (imports from src/_config/)
tailwind.config.js # Tailwind config (reads design tokens)
netlify.toml       # Netlify build + headers config
```

## Adding content

**New page** — add a `.md` or `.njk` file to `src/pages/` with front matter:
```yaml
---
title: Page Title
permalink: /page-slug/index.html
description: 'Short description for meta tags'
layout: page   # or base for full control
---
```
Then add it to `src/_data/navigation.js` if it belongs in the nav.

**New blog post** — add a `.md` file to `src/posts/`. Front matter inherits defaults from `posts.json`. Required fields: `title`, `date`.

**Navigation** — edit the `top` array in `src/_data/navigation.js`.

**Site-wide settings** — edit `src/_data/meta.js` (site name, description, author, blog RSS settings, theme colors).

## Brand Guidelines

The brand guidelines are located in `./docs/Scouting America Brand Guidelines-2024-BC.pdf`. Specificaly, the site should use the brand colors for Scouting America on pages 14 and 15.

## Key shortcodes and components

```njk
{% svg "misc/arrow-right" %}              {# inline SVG from src/assets/svg/ #}
{% image "path/to/img.jpg", "alt text" %} {# responsive image via @11ty/eleventy-img #}
{% year %}                                {# current year #}

<custom-youtube @slug="VIDEO_ID" @label="Title"></custom-youtube>
<custom-card>...</custom-card>
<custom-masonry>...</custom-masonry>
```

## Design system

Colors, spacing, type, and border-radius are defined as JSON tokens in `src/_data/designTokens/`. Tailwind and PostCSS both read these — edit the JSON, not Tailwind config directly. CSS follows CUBE CSS: compositions (`flow`, `grid`, `cluster`, `sidebar`), blocks, utilities.

## Environment

Copy `.env-sample` to `.env`. The `URL` variable is used in meta.js for absolute URLs (RSS, sitemap, OG images) — leave blank for local dev (defaults to `http://localhost:8080`).

## Planned pages

- `/events/` — Events / Calendar
- `/leadership/` — Leadership & Volunteers

## Units in Ames

- **Pack 159** — [Facebook](https://www.facebook.com/pack159ames/)
- **Pack 275** — [Facebook](https://www.facebook.com/pack275ames)
- Scouts BSA troops (TBD)
