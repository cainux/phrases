# Ljubljana Phrases

Offline Slovenian phrasebook PWA. Static files in `public/`, deployed to Cloudflare Workers (static assets) by GitHub Actions on every push to `main`.

## One-time setup
1. Create a Cloudflare API token from the **Edit Cloudflare Workers** template.
2. In this repo: Settings > Secrets and variables > Actions, add:
   - `CLOUDFLARE_API_TOKEN`
   - `CLOUDFLARE_ACCOUNT_ID` (Workers & Pages overview, right-hand sidebar)
3. Push to `main`. The site appears at `https://phrases.oha.me` (custom domain, configured in `wrangler.jsonc`; the `oha.me` zone must be on the same Cloudflare account).

## Updating
Bump `CACHE` in `public/sw.js` (e.g. `lj-phrases-v2`) when you change files, so installed copies refresh.

## Local preview
`npx wrangler dev`
