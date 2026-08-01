# R&R Cigars — Design Preview Site

Static HTML/CSS/JS wireframe of r-rcigars.com, for Red to click through and comment on
before final build. No framework, no build step — every page opens as-is.

## Pages

- `index.html` — Home landing page
- `login.html` — Member sign-in (simulated; redirects to order.html on "sign in")
- `order.html` — Order Ahead page (catalog, cart, pickup/locker details)
- `vendors/index.html` — Vendor directory (15 vendors, 2 with live example pages)
- `vendors/drew-estate.html`, `vendors/oliva.html` — Example vendor detail pages

Flow: Home → Order Ahead link → Login → (simulated sign-in) → Order Ahead → Our Selection → vendor page → back.

## Publish to preview.r-rcigars.com via GitHub Pages

1. Create a new GitHub repo (e.g. `rr-cigars-preview`). Public repo — GitHub Pages custom
   domains on private repos need a paid GitHub plan.
2. Push everything in this folder to the repo's `main` branch, at the root (not a subfolder).
3. In the repo: Settings → Pages → Build and deployment → Source: "Deploy from a branch" →
   Branch: `main` / `root` → Save.
4. Still in Settings → Pages, under "Custom domain" enter `preview.r-rcigars.com` and save.
   (The `CNAME` file already in this repo does this automatically too — GitHub will pick it up.)
5. Have John (holds the AWS Route 53 account for r-rcigars.com) add one DNS record —
   this is allowed even while the registrar transfer lock is active, since it's a DNS
   edit, not a registrar change:
   - Type: `CNAME`
   - Host/Name: `preview`
   - Value/Target: `<your-github-username>.github.io`
   - TTL: default
6. DNS usually propagates within minutes to a few hours. Once GitHub shows the domain as
   verified (green check on the Pages settings page), check "Enforce HTTPS."
7. Send Red the link: `https://preview.r-rcigars.com`

## Later: going live on the root domain

Once Red signs off on the design, this same content becomes the live site:
- If staying on GitHub Pages: use a separate repo (or a `main`/`prod` branch) with the
  `CNAME` file set to `r-rcigars.com` (apex) and `www.r-rcigars.com`, per the DNS record
  set already worked out — see the project notes for the exact A/CNAME records.
- If moving to Bluehost once the registrar transfer clears: no code changes needed — this
  is plain static files. Copy everything except `CNAME` and `README.md` into the host's
  public web root (e.g. `public_html/`), preserving the `vendors/` folder structure.
- Either way, the registrar transfer lock (clears ~Sept 11) does not block any of this —
  only the Bluehost *registrar* move itself.

## Known placeholders / not-yet-real in this preview

- Login is simulated — no real membership check yet (see the Auth & Inventory Integration
  Plan doc for the real design).
- Cart/order submission does not send anywhere yet — it's a UI walkthrough only.
- 13 of 15 vendor cards link to "#" — only Drew Estate and Oliva have example detail pages.
- Store hours on the Home/Order Ahead pages are still placeholder text.
