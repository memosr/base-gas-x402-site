# base-gas-x402 site

Static marketing/documentation site for the base-gas-x402 gas oracle. No build step, no framework, no server runtime. One HTML file plus assets.

```
index.html          the whole site
llms.txt            summary for agents that fetch it
robots.txt          allows everything, points at the sitemap
sitemap.xml         one URL
favicon.svg         blue circle-and-clock on dark
favicon.ico         16/32/48 fallback
apple-touch-icon.png
icon-512.png
og.png              1200x630 Open Graph / Twitter card
vercel.json         static config, cache and security headers
```

## Deploy

```bash
npx vercel --prod
```

Or drag the folder into the Vercel dashboard. Cloudflare Pages works the same way: no build command, output directory is the repo root.

## After the first deploy

1. Replace `https://base-gas-x402.vercel.app` in `index.html` (canonical, `og:url`, `og:image`, `twitter:image`), `robots.txt`, and `sitemap.xml` with the real URL. Five occurrences in `index.html`, one each in the other two.
2. Paste the URL into X and confirm the card renders `og.png`.
3. Reduce the API's `/` route to a redirect or a one-line pointer to this site, so the API stays a plain Node service.

## Notes

- The page is fully readable with JavaScript disabled. JS only powers the copy buttons and the live `/health` line.
- The `/health` widget reads the API's live coverage with `fetch` (the API allows any origin on its free routes). If the request fails, the static sentence stays. Nothing is faked.
- Prices in `index.html` and `llms.txt` are transcribed from `/openapi.json`. If the API's prices change, update both files. Verified against the live spec: `/gas` $0.002, `/gas/compare` $0.01, `/gas/history` $0.01, `/gas/cheapest-window` $0.02, `/health` free.
