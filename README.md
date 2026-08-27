# R&R Cigars — Design Preview Site

Static HTML/CSS/JS wireframe of r-rcigars.com, for Red to click through and comment on
before final build. No framework, no build step — every page opens as-is.

## Go-live scope

The first live release of r-rcigars.com is **Home, Visit Us, and Contact only** — the
Order Ahead flow (login → catalog/cart → vendor directory) is built and stays in this
repo, but is intentionally unlinked from the go-live nav until ordering is ready to
launch. Each go-live page's `<nav>` has the two ordering links commented out right next
to the live ones, so re-enabling ordering later is a one-line uncomment on `index.html`,
`visit.html`, and `contact.html` — the ordering pages themselves (`login.html`,
`order.html`, `vendors/*`) already link correctly to everything, including each other.
Note the ordering pages remain reachable by direct URL even while unlinked — this is a
"soft launch" hold-back, not access-controlled.

## Pages

- `index.html` — Home landing page. Nav: Home / Visit Us / Contact.
- `visit.html` — Visit Us: address, hours, phone, email, and an embedded Google map with
  a "Get Directions" link, for 5946 Osgood Ave N, Oak Park Heights, MN 55082.
- `contact.html` — Contact: email, phone, and location cards with quick email/directions actions.
- `login.html` — Member sign-in (simulated; redirects to order.html on "sign in"). Held back from go-live nav.
- `order.html` — Order Ahead page (catalog, cart, pickup/locker details, with the same
  Visit Us map embed). Held back from go-live nav.
- `vendors/index.html` — Vendor directory (15 vendors, 2 with live example pages). Held back from go-live nav.
- `vendors/drew-estate.html`, `vendors/oliva.html` — Example vendor detail pages. Held back from go-live nav.

Go-live flow: Home ↔ Visit Us ↔ Contact.
Ordering flow (not yet linked from go-live nav): Home → Order Ahead link → Login →
(simulated sign-in) → Order Ahead → Our Selection → vendor page → back.

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
- Store hours and the phone number are still placeholder text on Home, Visit Us, Contact,
  and Order Ahead — replace before flipping this to live.
- Contact page is email/phone/map only — no working contact form (would need a form
  backend like Formspree, since this is a static site with no server).
- The Visit Us / Order Ahead map is a keyless `google.com/maps?...&output=embed` iframe
  for 5946 Osgood Ave N, Oak Park Heights, MN 55082 — no API key or billing required.
  It's tinted (`filter: invert() hue-rotate()`) to sit against the dark theme instead of
  a stark white rectangle.
