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
- **Fonts:** Google Fonts (Space Grotesk for display/headings, Plus Jakarta Sans for body, JetBrains Mono for tech tags/monospaced items) are loaded via `<link>` in `<head>`.
- **Visual direction:** "Dark Fancy" — a premium, sleek developer aesthetic. Background is ultra-deep space blue-black (`#050811`) with subtle radial gradients and a 40px grid. Cards are glassmorphic, semitransparent with thin neon-tinted borders and background blurs. Accent colors are vibrant neon green (`--accent` `#00ff66`, used for glows, hover states, and active items) and amber (`--ember` `#ff8c00` as a secondary accent). Font stack uses Space Grotesk, Plus Jakarta Sans, and JetBrains Mono. Responsive layout, micro-animations (e.g. tilted profile photo on hover) are core.

