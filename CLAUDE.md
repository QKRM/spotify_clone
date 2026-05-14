# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file Spotify-inspired music player UI (`index.html`) — no build system, no dependencies, no package manager. Open the file directly in a browser to run it.

## Design System

All visual decisions are governed by `Design.md`. Read it before making any UI changes. Key rules:

- **Backgrounds**: `#121212` (page) → `#181818` (cards/sidebar) → `#1f1f1f` (interactive surfaces)
- **Accent**: Spotify Green `#1ed760` — only for play controls, active states, and primary CTAs. Never decorative.
- **Text**: `#ffffff` primary, `#b3b3b3` secondary/muted
- **Buttons**: always pill-shaped (`border-radius: 9999px` small, `500px` large, `50%` circular play buttons). Never square.
- **Button labels**: `text-transform: uppercase` + `letter-spacing: 1.4px–2px` + `font-weight: 700`
- **Shadows**: heavy on dark backgrounds — `rgba(0,0,0,0.3) 0px 8px 8px` (cards), `rgba(0,0,0,0.5) 0px 8px 24px` (dialogs)
- **Input borders**: inset shadow combo — `rgb(18,18,18) 0px 1px 0px, rgb(124,124,124) 0px 0px 0px 1px inset`
- **Typography range**: 10px–24px. Compact and dense — not a marketing site.

## Architecture

`index.html` is self-contained: CSS in `<style>`, markup in `<body>`, interactivity in `<script>`.

**Layout grid** (CSS Grid, 3 zones):
- `grid-template-columns: var(--sidebar-w) 1fr` + `grid-template-rows: 1fr var(--player-h)`
- Sidebar (`.sidebar`) — fixed-width left nav + library
- Main (`.main`) — scrollable content area with topbar, cards, track list
- Player footer (`.player`) — spans full width, `grid-column: 1 / -1`

**CSS custom properties** (defined on `:root`): all colors, sidebar width (`--sidebar-w: 240px`), player height (`--player-h: 90px`), and shadow values are tokenized — change tokens, not raw values.

**Responsive breakpoints** (in `<style>`):
- `≤1024px`: sidebar collapses to icon-only (72px), card grid → 3 columns
- `≤768px`: sidebar hidden, card grid → 2 columns, featured title shrinks

**JS interactions** (inline `<script>`, ~30 lines):
- Tag filter active state toggle
- Play/pause button icon swap
- Progress bar click-to-seek
- Volume bar click-to-set
