# Tempo: deploy to Cloudflare Pages (free plan)

Files: `index.html` (the whole app), `_headers` (security headers), `manifest.webmanifest`, `sw.js`, and two icons (offline install). No build step, no server, no database.

## Deploy (pick one)
1. **Dashboard upload (easiest, no Git, no build):** Cloudflare dashboard > Workers & Pages > Create > Pages > Upload assets > name the project > drag in this folder > Deploy. Your site is `https://<project>.pages.dev` with HTTPS. To update, create a new deployment and upload again.
2. **GitHub:** push this folder to a repo, connect it in Pages. Framework preset: None. Build command: empty. Output directory: the folder that holds `index.html`. Every push counts as a build.
3. **CLI:** `npx wrangler pages deploy tempo-site --project-name tempo`

## Free plan limits (from Cloudflare's Pages limits page)
| Limit | Free plan | Tempo uses |
|---|---|---|
| Files per site | 20,000 | 6 |
| Max size of one file | 25 MiB | about 0.1 MiB |
| Git builds per month | 500 (one at a time, 20 min timeout) | 0 with dashboard upload |
| Custom domains per project | 100 | 0 to 1 |
| `_headers` | 100 rules, 2,000 characters per header | 6 headers in 2 rules, longest about 330 characters |
| Projects per account | 100 | 1 |

## Notes
- HTTPS is automatic, which microphone recording in Dictation needs.
- Fonts load from Google Fonts. If you self-host them, update `font-src` and `style-src` in `_headers`.
- The Content-Security-Policy only allows requests to the site's own address (needed by the offline service worker), so the app cannot send data to any other server.
- **Install as an app:** on Chrome or Edge use the install icon in the address bar; on iPhone use Share > Add to Home Screen. After the first visit it also opens offline (fonts fall back to system fonts).
- When you change `index.html`, bump `V` in `sw.js` (for example `tempo-v4`) so installed copies refresh.
- All data (questions, scores, recordings) stays in the visitor's browser. The footer has a button to erase it.

## Tests
- `node tempo-unit.js index.html` (logic)
- `python3 tempo-e2e.py` (browser; needs `pip install playwright` and `playwright install chromium`; edit the URL at the top)

## For your portfolio
Show: the problem (typing practice from your own questions), the accessibility work (WCAG AA contrast, keyboard use, 44px targets), the testing (unit plus browser checks), and the constraints you designed for (single static file, free hosting, no data leaves the device).
