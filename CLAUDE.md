# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A Jekyll-based static site for the "Desarrollo de Software" (DDSO) course at UTN. It is deployed to GitHub Pages at `https://ddso-utn.github.io`.

## Commands

```bash
# Install dependencies
bundle install

# Serve locally with live reload
bundle exec jekyll serve

# Build the static site
bundle exec jekyll build
```

## Site architecture

The site uses a custom Jekyll theme (not a standard gem-based theme — layouts and includes are in the repo itself).

**Key directories:**
- `_layouts/` — two layouts: `home.html` (the landing page) and `page.html` (all other pages)
- `_includes/` — reusable partials: `head.html`, `header.html`, `footer.html`, `pseudofooter.html`, `tooltip.html`, `javascripts.html`
- `pages/` — all content pages organized as:
  - `bitacoras/` — per-course-run class logs, nested by semester (e.g. `2025-2c/`) and then by commission (e.g. `jueves-manana/`). Each commission has an index `.md` and a subdirectory of per-class pages (`clase01.md`, `clase02.md`, …)
  - `pautas/` — course guidelines (cursada, parciales, trabajos prácticos)
  - `apuntes/` — reference notes and topic pages
- `attachments/` — static files (PDFs, etc.) served directly

**Front matter conventions:**
- All content pages use `layout: page`
- The landing page (`index.md`) uses `layout: home`
- Bitácora index pages embed a Google Sheets iframe via the `frame:` front matter key
- Permalinks use hyphens even when the filename uses no separator (e.g. file `clase01.md` → permalink `/clase-01/`)

**`_config.yml` notable settings:**
- `tooltip-enabled: false` — the tooltip feature is off by default; set to `true` and configure `tooltip-label`/`tooltip-link` to enable it
- `baseurl: ""` — site is served from the root

## Content conventions

- Class pages (`clase0N.md`) follow the structure: Bienvenida / Quiénes Somos / Temario / Resumen / Material / Tarea
- Internal links between pages use relative Markdown paths (e.g. `../../../pautas/sobre-los-parciales.md`) or `{{site.baseurl}}/…` in HTML layouts
- PlantUML diagrams are embedded as external image URLs (`https://www.plantuml.com/plantuml/png/…`)
