# amazon-operator-stack — guided setup

A privacy-by-design web wizard that walks Amazon sellers through SP-API credential capture. Designed as a **take-home** companion to the Seller Sessions Live 2026 stage demo.

**Live:** https://amazon-operator-stack-setup.vercel.app *(deployed from `main`)*

**CLI repo:** https://github.com/ShubhashSharma/amazon-operator-stack

## What it does

A single-page web form that mirrors the 7 steps of the CLI wizard (`npm run setup` in the main repo). Attendees take it home, work through it at their own pace, and at the end download a working `.env` file plus a single copy-paste command that clones the repo, drops the `.env` in place, and wires it into Claude Code.

## Take-home robustness

Designed for unattended async use. Three things make it survive:

- **Autosave badge.** A "✓ Saved" pill pulses on every change, then settles into "Saved Xs / m / h ago". If `localStorage` is full or disabled (incognito, restrictive policies), it switches to "Save failed" in red — no silent loss.
- **Backup + restore.** Two discreet links at the bottom: "Save backup" downloads `aos-progress-YYYY-MM-DD-HHmm.json`, "Restore from backup" reads it back. Belt + braces for cleared caches, switched browsers, accidental resets.
- **One-paste finish.** Step 7 generates a single bash (or PowerShell) block that clones the repo if needed, drops the `.env` in place, runs `npm install`, runs the smoke-test, and wires the MCP server into Claude Code. Auto-detects OS, copyable with one click (with text-selection fallback if the clipboard API fails).

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
