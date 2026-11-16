# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

Offline Slovenian phrasebook PWA ("Ljubljana Phrases"). No build step, no package.json, no tests, no linter: everything served is a static file in `public/`. Deployed as Cloudflare Workers static assets (`wrangler.jsonc`, worker name `phrases`, custom domain `phrases.oha.me`) by `.github/workflows/deploy.yml` on every push to `main`.

## Commands

- Local preview: `npx wrangler dev`
- Deploy: push to `main` (needs `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID` repo secrets). Manual: `npx wrangler deploy`.

## Architecture

- `public/index.html` is the whole app: inline `<style>` and one inline `<script>`. Phrase content lives in the `DATA` array. A section is either `{t, open?, items: [[slovenian, pronunciation, english], ...]}` or `{t, notes: [html strings]}`. Notes sections are hidden while searching, and their strings are inserted as raw HTML, unlike item text, which goes through `esc()`.
- `render(filter)` rebuilds the DOM on every search keystroke. `norm()` strips diacritics (č/š/ž, etc.) so searches match without them.
- `public/sw.js` is a cache-first service worker that refreshes the cache in the background. It precaches the fixed `ASSETS` list.
- `public/_headers` sets `no-cache` on `sw.js` and `index.html`, so updates are picked up.

## Gotchas

- **Bump `CACHE` in `public/sw.js`** (e.g. `lj-phrases-v1` → `v2`) whenever you change any cached file. Installed copies serve the old cache until it changes.
- If you add a new static asset, add it to `ASSETS` in `sw.js` or it won't be available offline.
- The `oha.me` zone must be on the same Cloudflare account for the custom-domain route to work.
