# hossein-bozorg-zadeh.github.io

Personal portfolio, live at **https://hossein-bozorg-zadeh.github.io** — a static
site (plain HTML/CSS/JS, no build step, no dependencies) that automatically
mirrors the repositories pinned on the
[GitHub profile](https://github.com/hossein-bozorg-zadeh).

## How the auto-sync works

The site never needs to be edited by hand. It reads `pinned.json`:

1. **Pin or unpin repos on your GitHub profile** (the "Pinned" section).
2. The [`refresh-pinned`](.github/workflows/refresh-pinned.yml) GitHub Action
   runs **every 6 hours** (or anytime via *Actions → Refresh pinned repos → Run
   workflow*) and rewrites `pinned.json` from the GraphQL API — profile name,
   bio, avatar, stats and the pinned repositories with their descriptions,
   languages, stars and links.
3. If `pinned.json` changed, the Action commits it and GitHub Pages redeploys.

If the GraphQL call ever fails, the workflow falls back to the public REST API
(top 6 non-fork repos) and the page shows a small "temporarily unavailable"
note until the next successful sync.

Everything else on the page (colors, tagline, layout) is edited directly in
`index.html`. The tagline shown under the name is the GitHub bio — set a bio on
your profile and it will appear here on the next sync; until then a default
line is used.

## Local preview

```bash
python3 -m http.server 8080
# open http://localhost:8080
```

Serving over HTTP is required for `fetch("pinned.json")` to work
(`file://` pages cannot fetch).
