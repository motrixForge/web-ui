# motrix-forge-web

Static site for **Motrix Forge** — a small independent puzzle game studio.
Our first title, **Block Craft**, is in development.

Deployed to GitHub Pages at <https://motrixforge.com>.

No build step, no dependencies. Plain HTML, CSS and vanilla JS.

## Structure

```
index.html                 # single-page site (hero, Block Craft, studio, process, contact)
404.html                   # custom not-found page
favicon.svg
CNAME                      # motrixforge.com — required for the custom domain
.nojekyll                  # serve files as-is (no Jekyll processing)
robots.txt / sitemap.xml
assets/css/style.css
assets/js/main.js          # nav, scroll reveal
.github/workflows/deploy.yml
```

## Local preview

Open `index.html` directly, or serve it so root-absolute paths (`/assets/...`) resolve:

```bash
python -m http.server 8000
# http://localhost:8000
```

## Deploy

Every push to `main` triggers `.github/workflows/deploy.yml`, which uploads the
repo root as a Pages artifact and publishes it.

**One-time setup in the repo:**

1. Settings → Pages → **Source: GitHub Actions**.
2. Settings → Pages → Custom domain → `motrixforge.com` → Save.
3. Tick **Enforce HTTPS** once the certificate is issued (can take up to ~24h).

## DNS records at the registrar

Apex domain `motrixforge.com` → four `A` records (and optionally the `AAAA` set):

| Type | Name | Value |
|------|------|-------|
| A    | @    | 185.199.108.153 |
| A    | @    | 185.199.109.153 |
| A    | @    | 185.199.110.153 |
| A    | @    | 185.199.111.153 |
| AAAA | @    | 2606:50c0:8000::153 |
| AAAA | @    | 2606:50c0:8001::153 |
| AAAA | @    | 2606:50c0:8002::153 |
| AAAA | @    | 2606:50c0:8003::153 |
| CNAME| www  | ericnguyen030215.github.io. |

Keep `CNAME` in the repo — GitHub rewrites it when you change the domain in
Settings, and deleting it drops the custom domain on the next deploy.

## Editing content

Block Craft lives in the `#game` section of `index.html`. Its artwork is a pure-CSS
placeholder pattern (`.art-1` in `style.css`) — swap the `<div class="feature-art">`
for an `<img>` once there are real screenshots.

The copy deliberately makes no claims we can't back up: no download counts, no
release date, no back catalogue. When Block Craft ships, add the store links and a
second section rather than inflating this one.
