# Tenth House — website

The public site for Tenth House (**10thhouse.org**). One self-contained static page — no build step, no dependencies, no framework. It can't "break" from a failed script, and it hosts anywhere.

## Files
- `index.html` — the entire site (HTML + inline CSS).
- `favicon.svg` — browser-tab icon.
- `og-image.svg` / `og-image.png` — the social-link preview card (1200×630). If `og-image.png` is missing, export the SVG to PNG once (any browser screenshot or an online SVG→PNG converter).
- `CNAME` — tells GitHub Pages the custom domain (`10thhouse.org`).

## Hosting — GitHub Pages, with the Squarespace-registered domain pointed at it
1. Put these files in a public GitHub repo (e.g. `tenth-house-site`).
2. Repo → **Settings → Pages → Source: deploy from `main` (root)**.
3. The `CNAME` file sets the custom domain to `10thhouse.org`.
4. At **Squarespace** (where the domain is registered) → the domain's **DNS settings**, add:
   - **A** records for `@`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
   - **CNAME** `www` → `<your-github-username>.github.io`
5. Wait for DNS + GitHub's SSL (up to ~24–48h), then tick **Enforce HTTPS**.

*(No Cloudflare needed — the domain stays at Squarespace; GitHub only serves the files.)*

## Maintenance
Edit `index.html` and push to `main`; GitHub Pages redeploys automatically. Dwith can edit the files in the local `Tenth_House/Website/` folder; committing + pushing to the repo updates the live site. This is the "versioned foundation" — every change is tracked and reversible.
