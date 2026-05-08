# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static HTML/CSS personal portfolio website for Himanshu Sachan ("Joker"), deployed on Netlify at `joker-himanshu-portfolio.netlify.app`. There is no build system, no JavaScript framework, and no package manager — all pages are plain HTML files linked to a single stylesheet.

## Development

**To view the site locally**, serve files with any static HTTP server (internal links use absolute paths like `/index.html` so opening HTML files directly from the filesystem will break navigation):

```bash
npx serve .
# or
python3 -m http.server 8080
```

There are no build, lint, or test commands.

## Architecture

### Pages
| File | Purpose |
|---|---|
| `index.html` | Home — hero, bio summary, projects list, blogs list, footer |
| `about.html` | Full about page with profile photo and bio |
| `projects.html` | Projects showcase |
| `blogs.html` | Blog index with previews linking to individual posts |
| `blog1.html` | "Value Investing guide for Beginners" |
| `blog2.html` | "#Mistakes I Shouldn't Make as a stock Investor" |
| `libdir/composite.html` | Component reference page (not linked from nav) |

### Styling (`styles.css`)
Single stylesheet shared by all pages. Key conventions:
- CSS custom properties are declared on `:root` — always use these vars (`--purple`, `--yellow`, `--primary-color: #6C63FF`, etc.) rather than raw hex values.
- Google Fonts: Montserrat (weight 500) is the sole typeface, loaded via `@import`.
- Responsive breakpoint at `max-width: 700px` at the bottom of the file.

### Two Navigation Variants
There are two distinct nav styles that must not be mixed:
- **`.Navigation`** — used only on `index.html`; has the hero/background-image treatment and larger main-content block.
- **`.Navigation-1`** — used on all other pages (`about.html`, `projects.html`, `blogs.html`, blog posts); same background image but compact layout.

Both navs share the inner `.menu-list` / `.menu` / `.link` classes for the list items.

### Asset Paths
All internal `href` and `src` values use **absolute paths** (e.g. `/images/favicon.ico`, `/index.html`). Keep this convention — relative paths will break when deployed under a sub-path.

The profile photo in `about.html` is hotlinked from LinkedIn CDN and may expire; replace with a locally hosted image in `images/` if it breaks.

### Component Library
`libdir/composite.html` is a living style guide / component sandbox. It references `main.css` and `main.js` which are not present in the repo (future additions). It also links `../styles.css` — if styles.css is renamed or moved, update this reference too.

## Branch Notes

The active content lives on the **`master`** branch. The `main` branch is empty (only a stub README). Always base new work off `master`.
