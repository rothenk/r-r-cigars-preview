# R&R Cigars — Email Templates

Two ready-to-use templates, both built from the real logo artwork and the confirmed
business address (5946 Osgood Ave N, Oak Park Heights, MN 55082).

## 1. `signature.html` — Gmail signature

A one-time-setup signature block with the logo, name/title line, address, phone, and
email, in R&R's red/gold branding. The logo is embedded directly in the file (as a
data URI) so it survives copy-paste with no external image dependency.

**Install:**
1. Open `signature.html` in a browser (double-click it).
2. Click inside the signature, press Ctrl/Cmd+A to select all, then Ctrl/Cmd+C to copy.
3. Gmail → Settings (gear) → "See all settings" → General → Signature → "Create new" →
   click into the empty box → Ctrl/Cmd+V to paste → scroll down → Save Changes.
4. Before pasting, edit the `Red [Last Name]` line and `[Phone number]` link in the
   file for whoever is setting it up — each person who wants this signature needs their
   own name/title on that line.

Repeat per Gmail account. Outlook and Apple Mail have their own signature editors but
accept the same copy-paste approach.

## 2. `email-template.html` — Announcement / newsletter template

A full HTML email layout (header with logo → headline → body copy → button → footer
with store info) for one-off sends: new arrivals, events, promotions, seasonal updates —
this is the same shape Red's transition-pricing announcement would use going forward.

Built with an HTML-table layout (not CSS grid/flexbox) because that's still what
renders reliably across Outlook, Gmail, and Apple Mail — email clients lag years behind
browsers on CSS support.

**Placeholders to fill in per send** (all in brackets):
- `[Announcement headline goes here]`
- The body paragraph under "Hi [First Name],"
- `[Button text, e.g. Visit Us]` and its link target
- `[Phone number]` in the footer (same placeholder still pending from Red)
- `{{unsubscribe_link}}` — see note below

**Before sending any real campaign:**
- This template references the logo at `https://preview.r-rcigars.com/images/rr-logo-email.png`.
  `images/rr-logo-email.png` is included in this folder — upload it into the `images/`
  folder of the preview GitHub repo (same web-upload method used for the other site
  files) so that URL resolves. Once r-rcigars.com is live on Bluehost, switch the `src`
  to `https://r-rcigars.com/images/rr-logo-email.png` instead.
- Email templates aren't pasted into Gmail like the signature — they're meant to be
  loaded into a sending tool (Mailchimp, Constant Contact, Formspree partner tools, or
  Gmail's "Insert HTML" via a browser extension). Plain Gmail compose doesn't accept
  raw HTML paste the way its signature box does.
- The footer's physical address and an unsubscribe link are a CAN-SPAM requirement for
  any commercial/promotional email in the US — keep both on every send. The
  `{{unsubscribe_link}}` placeholder is written in the merge-tag style most sending
  platforms use; replace it with whatever your platform's actual unsubscribe tag or URL
  is.

## Logo asset

`images/rr-logo-email.png` — the R&R Cigars wordmark, trimmed and exported with a
transparent background at 640×341px, sourced from the vector logo
(`R & R and Reds Lounge/Artifacts/R & R1.svg`) already in the project files. This is a
different, higher-resolution export than any logo currently on the live site pages, so
if you want it there too (e.g. as a favicon or header mark) just say so.
