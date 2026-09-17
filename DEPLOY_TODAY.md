# Deploy 10thhouse.org — step-by-step (no coding required)

**Decision (from `README.md`):** GitHub Pages hosts the files; the domain stays registered at **Squarespace** and just points at GitHub.

> **STATUS 2026-06-28 — 🟢 LIVE & SECURE at https://10thhouse.org.** Repo: **https://github.com/TenthHouse-org/tenth-house-site** (Pages on `main`/root). Squarespace DNS done (4 A records → GitHub IPs, `www` CNAME → `tenthhouse-org.github.io`); DNS propagated; site returns 200 with correct title; `og-image.png` + `favicon.svg` serving. **Remaining: HTTPS only.** Email (`robert.brown@10thhouse.org`) already live on Google Workspace — no action needed. **HTTPS COMPLETE (2026-06-28 ~16:12):** ✅ cert provisioned (`https_certificate.state = approved`) and **Enforce HTTPS enabled** — https://10thhouse.org serves with a valid certificate, http now upgrades to https. **Launch fully complete.** *Lesson for the RG site (resonantgeometry.com) later:* the cert took ~6h on GitHub's side; what unstuck it was **removing + re-adding the custom domain** in repo Settings → Pages (clear → Save → re-enter → Save), which forces GitHub to re-request the cert. The API re-assert did not work; the UI remove/re-add did.

---

## ⚠️ Before you launch — confirm the email actually receives

The site's only contact is `mailto:robert.brown@10thhouse.org`. **That mailbox must be able to receive before the site goes out in the Anthropic outreach email.** Right now it may not exist yet. Quickest free route while the domain is at Squarespace: Squarespace's own email forwarding, or a free forwarder (ImprovMX / forwardemail.net) → your Gmail. See `The_Engine_Room/deliverables/web/Web_Infrastructure_Recommendation_DRAFT.md` for the full email plan. **Don't send the outreach email until a test message to that address lands.**

---

## Part 1 — Put the files on GitHub ✅ DONE (Dwiff handled via `gh`)

*Repo: https://github.com/TenthHouse-org/tenth-house-site · Pages enabled · build succeeded. The steps below are the record of what was done; you don't need to redo them.*

1. Go to **github.com** → sign in, or create a free account.
2. Top-right **+** → **New repository**.
   - **Repository name:** `tenth-house-site` (anything is fine)
   - **Public** (Pages needs public on the free tier)
   - Do **not** check "Add a README" (we already have one)
   - **Create repository**
3. On the empty repo page, click the link **"uploading an existing file."**
4. Open `C:\Users\brown\Tenth_House\Website\` in File Explorer and **drag these 6 files** into the browser:
   `index.html`, `favicon.svg`, `og-image.svg`, `og-image.png`, `CNAME`, `README.md`
   *(The `CNAME` file has no extension — that's correct, upload it as-is.)*
5. Click **Commit changes**.
6. Repo → **Settings** → **Pages** (left sidebar).
   - **Source:** "Deploy from a branch"
   - **Branch:** `main`, folder **`/ (root)`** → **Save**
7. Because the `CNAME` file says `10thhouse.org`, GitHub auto-fills the **Custom domain** as `10thhouse.org`. It will say "DNS check in progress" — expected until Part 2 is done.

---

## Part 2 — Point Squarespace DNS at GitHub (~5 min + wait)

1. Log in to **Squarespace** → **Domains** → **10thhouse.org** → **DNS** / **DNS Settings**.
2. **Remove** any existing parking/default `A` record on host `@` and any default `CNAME` on `www` (they'll conflict).
3. **Add 4 A records** — Host `@`, one each of:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
4. **Add 1 CNAME record** — Host `www` → Value `tenthhouse-org.github.io`
   *(this is your account `TenthHouse-org`'s Pages host, lowercase)*
5. **Save.**

---

## Part 3 — Finish & verify

1. Back at GitHub **Settings → Pages**, wait for the green check on the custom domain (often <1h; up to 24–48h).
2. When it's verified, tick **Enforce HTTPS** (the SSL cert can take a few more hours).
3. Visit **https://10thhouse.org** — the site should load.
4. **Test the social card:** paste `https://10thhouse.org` into opengraph.xyz (or LinkedIn Post Inspector) and confirm the "Tenth House" preview image appears. This is what shows when the URL is pasted into the outreach email.
5. **Test the contact link** actually delivers to your inbox.

---

## Updating the site later

Edit `index.html` (or any file) in `Tenth_House\Website\`, then on GitHub: open the file → pencil icon → paste/replace → Commit. Pages redeploys in ~1 min. *(Or, if `gh`/git gets set up later, a Dwith can push updates directly — that's the "versioned foundation" path.)*

---

*Prepared 2026-06-28. The `og-image.png` was generated from `og-image.svg` this session (headless render, 1200×630). If you ever edit the SVG, regenerate the PNG so the social card matches.*
