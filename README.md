# amazon-operator-stack — guided setup

A privacy-by-design web wizard that walks Amazon sellers through SP-API credential capture, alongside the Saturday Seller Sessions Live 2026 stage demo.

**Live:** https://amazon-operator-stack-setup.vercel.app *(deployed from `main`)*

**CLI repo:** https://github.com/ShubhashSharma/amazon-operator-stack

## What it does

A single-page web form that mirrors the 7 steps of the CLI wizard (`npm run setup` in the main repo). Attendees follow Shubhash on stage as he walks through Seller Central, paste their values into each step, and at the end download a working `.env` file they drop into the cloned CLI repo.

| Step | What the attendee does |
|------|------------------------|
| 1 | Reads the welcome + prerequisites |
| 2 | Picks their Amazon region (EU / NA / FE) |
| 3 | Picks their primary marketplace + ticks any others they sell on |
| 4 | Registers as a developer in Seller Central, creates an SP-API app, pastes Client ID + Secret |
| 5 | Clicks "Authorize" in Seller Central, pastes the refresh token |
| 6 | Reviews the summary |
| 7 | Downloads `.env`, runs three CLI commands |

## Privacy

- **No backend.** The page is a single static HTML file. There is no server-side code.
- **No tracking, no analytics.** Source-viewable, MIT licensed.
- **State persists in `localStorage` only** — never sent anywhere.
- **The `.env` file is generated client-side via a `Blob`** and downloaded directly. Refresh tokens never leave the attendee's browser.

## Local dev

```bash
git clone https://github.com/ShubhashSharma/amazon-operator-stack-setup.git
cd amazon-operator-stack-setup
open index.html        # Mac
# or just point any local web server at this directory
```

No build step. No npm install. Open `index.html` in a browser and it works.

## Deploy

Vercel auto-deploys from `main`. The whole project is one static HTML file plus this README. `vercel.json` sets the project to static-site mode.

## License

MIT — same as the CLI repo.
