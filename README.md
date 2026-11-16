# Ljubljana Phrases

Offline Slovenian phrasebook PWA. Static files in `public/`, deployed to Cloudflare Workers (static assets) by Cloudflare's Git integration (Workers Builds) on every push to `main`.

## Deployment
The `phrases` worker is connected to this repo in the Cloudflare dashboard and runs `npx wrangler deploy` on each push. Build status shows as a "Workers Builds: phrases" check on commits. The site is at `https://phrases.oha.me` (custom domain, configured in `wrangler.jsonc`; the `oha.me` zone must be on the same Cloudflare account).

## Updating
Bump `CACHE` in `public/sw.js` (e.g. `lj-phrases-v2`) when you change files, so installed copies refresh.

## Local preview
`npx wrangler dev`
