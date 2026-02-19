# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build & Development

```bash
npm install          # Install Bulma CSS from npm
npm run build        # Copy bulma.min.css from node_modules into css/
```

The site uses absolute CSS paths (`/css/bulma.min.css`), so opening `index.html` via `file://` won't load styles. Use a local server:
- **VS Code Live Server**: right-click `index.html` → "Open with Live Server"
- **Terminal**: `npx serve .`

There are no tests, no linter, no bundler. The only build step copies one CSS file.

## Deployment

Deployed to Netlify. Config in `netlify.toml`:
- Build command: `npm install && npm run build`
- Publish directory: `.` (repo root, no `dist/` folder)
- Deploys automatically on push to `main`

## Architecture

Static HTML/CSS site. No JavaScript framework, no server, no templating.

- **Bulma v1.0.4** (npm) — CSS framework for layout and components
- **Font Awesome v6.5** (CDN) — icons throughout the site
- **`css/custom.css`** — gradients, shadows, hover animations, scroll fade-ins layered on top of Bulma

### Pages

- `index.html` — main page: navbar, hero, work experience, education, project card grid, footer
- `projects/project-1.html` — project detail: screenshot, overview, tech stack tags, feature list, links
- `projects/project-2.html` — same structure, different content

### Key conventions

- Navbar and footer are **duplicated** across all pages. Changes must be applied to every HTML file.
- `css/bulma.min.css` is **generated** by `npm run build` — never edit it directly.
- CSS custom properties in `custom.css` define the theme: `--gradient-primary`, `--gradient-dark`, `--shadow-card`, `--transition-base`, etc.
- Scroll animations use the `animate-on-scroll` class with an IntersectionObserver in `<script>` tags.
- Projects grid supports up to 6 cards (3 per row via `column is-one-third`).

### Adding a new project

1. Copy an existing `projects/project-N.html`
2. Update content (hero, overview, tech tags, features, screenshot URL)
3. Add a card in the `#projects` section of `index.html`
4. Add a navbar dropdown link in **all** HTML files
