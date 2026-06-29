# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Static, single-page personal link hub for Huskynarr, hosted on GitHub Pages. Pure HTML/CSS with a small inline `<script>` — **no build step, no package manager, no framework, no dependencies**. The entire site is `index.html` + `css/style.css`.

## Development & Deployment

- **Preview locally:** open `index.html` directly in a browser, or serve the directory (`python3 -m http.server`). There are no tests, linters, or build commands.
- **Deploy:** push to `main`. GitHub Pages auto-deploys from the root of the `main` branch.
- **Custom domain:** the `CNAME` file controls the live domain (currently `huskynarr.is-a.dev`). Note this differs from `huskynarr.de` referenced throughout the content — `huskynar.de`/`huskynarr.de` is the author's separate main site, not this repo's host.

## Architecture

The page is a tabbed interface driven entirely by CSS class toggling — there is no router or state library.

- **`index.html`** holds all content and structure:
  - A profile header (`.profile-card`).
  - A tab navigation (`.tab-navigation`) with two panels: **Projekte** (`#projects-panel`) and **Socials & Links** (`#socials-panel`).
  - Each project/link is a self-contained, comment-labeled block (e.g. `<!-- Project 9: Autism Tests Platform -->`, `<!-- Link 5: YouTube -->`). Adding an entry means copying an existing sibling block and editing it.
  - The inline `switchTab(tabName)` script at the bottom toggles the `active` class on `.tab-panel` and `.tab-button` elements. `data-tab` on the button must match the `<panel>-panel` id.
- **`css/style.css`** is a single external stylesheet. Panel visibility is controlled by `.tab-panel` / `.tab-panel.active`; only the active panel is shown.

## Content conventions

- **Language:** all user-facing copy is German (`<html lang="de">`). Match this when editing visible text.
- **Logo fallback:** `images/logo.svg` is referenced locally with an `onerror` fallback to the remote `https://huskynarr.de/_nuxt/logo.H2Zu-rsI.svg`. The local SVG must be downloaded separately (see `images/README.md`); it may be absent in a fresh clone, which is why the fallback exists.
- **SEO/social:** keep the `<title>`, `<meta name="description">`, and Open Graph tags in `<head>` in sync when the site's purpose or branding changes.
- **Fonts:** Google Fonts (Bricolage Grotesque for display/headings, Hanken Grotesk for body) are loaded via `<link>` in `<head>`.
- **Visual direction:** "Husky Atelier" — a light, warm theme built on the brand green. The bright logo lime (`--leaf` `#98c32f`) is used for accent pops (avatar border, hover borders); a darker readable green (`--frost` `#5c7a16`, AA-contrast on white) is used for icons, links, and solid fills with white text; warm amber (`--ember`) is the secondary accent (name underline, status dot). All colors are CSS custom properties in `:root`. Avoid reintroducing the old dark "cyber" look (neon glow, grid backgrounds, fake "SYSTEM ONLINE" telemetry).
