# AGENTS.md

This file provides guidance to Codex (Codex.ai/code) when working with code in this repository.

## Project Overview

Jainverse (jainverse.in) is a static website introducing Jainism to beginners. It is hosted via GitHub Pages with a custom domain. There is no build system, bundler, or framework — every page is a self-contained HTML file with inline CSS and JS.

## Architecture

- **Landing page**: `index.html` — homepage with hero, project cards, and trilingual i18n (Marathi/Hindi/English)
- **Philosophy journey**: A sequence of self-contained pages at `/<topic>/index.html`, each covering one concept in the arc from soul → karma → liberation. Current pages: `jeev-ajeev`, `ajiva`, `karma`, `kashaya`, `ashrav-bandh`, `samvar-nirjara`, `moksha`
- **Summary/map page**: `summary/index.html` — overview of the journey so far
- **Jambudweep**: `jambudweep/index.html` — interactive 3D map of Jain cosmological geography (uses Three.js via CDN, separate visual style from philosophy pages)

Each philosophy page duplicates its own CSS/JS and i18n strings (no shared stylesheet or component system). When changing shared design elements (colors, fonts, nav), you must update each file individually.

## Design System (duplicated per file)

- **CSS variables**: `--saffron`, `--indigo`, `--gold`, `--sand`, `--warm-white`, `--stone`, `--text` families
- **Fonts**: DM Serif Display (headings), Instrument Sans (body), Tiro Devanagari Hindi (Devanagari text) — loaded from Google Fonts
- **i18n**: Client-side via `data-i18n` attributes and a `const i18n = { mr: {}, hi: {}, en: {} }` object per page. Language persisted in `localStorage('jainverse-lang')`, default is Marathi.

## Content Guidelines

- **Tradition**: Digambar. Do not mix in Shvetambar-specific practices.
- **Philosophical accuracy**: Good karma (punya) is NOT "lighter" — it's a different type of bondage (gold chain vs iron chain). The goal is to shed ALL karma, not accumulate good karma.
- **Pedagogy**: Explain concepts in simple everyday language first, then introduce Sanskrit/Prakrit terminology. Don't frontload jargon.
- **Language**: Keep Marathi/Hindi colloquial. English loanwords (like "interactive", "3D") are fine where natural.
- **Diagrams**: Only add if they genuinely aid understanding — don't force visuals.
- **Homepage**: Don't add new cards/links to the homepage unless explicitly asked.

## Development

No build step. To preview locally, serve the directory with any static server:

```
python3 -m http.server 8000
# or
npx serve .
```

Pages use absolute paths (`/jeev-ajeev/`) for inter-page links, so a local server is needed (file:// won't work for navigation).
