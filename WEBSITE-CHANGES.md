# Website Changes — 2026-10-05

## Update (same day) — Formspree online form merged in
Merged `Patch-and-Paint-Bros-ONLINE-FORM-UPDATE.zip` (built with ChatGPT) into this project. That package turned out to be built directly from these exact files, so the diff was small and clean — not a redesign. Kept:
- Real online form submission via Formspree (`action="https://formspree.io/f/moejqzkp"`), AJAX with Sending/disabled-button state, success and error messages exactly as specified, no page reload, customer never leaves the site.
- Removed `autoplay` from both homepage videos per the new "visitor decides when to play" rule (they were muted before, but now also don't auto-start at all).
- Fixed genuinely stale copy ("will be featured here" → describes what's actually shown).
- Removed the gold 5-star icon from the reviews placeholder (text-only "coming soon" now — more clearly not a real rating).
- Hid social icons entirely instead of leaving `href="#"` dead links.
- Added Escape-to-close and proper `aria-expanded`/`aria-label` toggling on the mobile menu.
- Removed the old `mailto:`-generating JS from `index.html` (replaced by Formspree) and deleted a leftover dead copy of that same script sitting unused in `gallery.html`.

**One real bug caught and fixed during merge:** the new `privacy.html` added a correct "processed by Formspree" disclosure, but left the *old* paragraph in place still claiming the form "opens a pre-filled email... not stored on a server anywhere" — directly contradicting the new section right below it. Rewrote the How-the-form-works / Third-parties / How-long-we-keep-it sections so the policy is internally consistent and accurate to what the form now actually does.

Also removed the "Owner input required" callout (which named Sylvia by name) from the public `terms.html`, and the internal reviewer note from `privacy.html` — both were fine for a draft but not meant for visitors. The actual substance (not inventing deposit/cancellation/refund terms) is preserved in the Estimates section's plain-language line instead.

**Tested before opening for review:** intercepted the real Formspree request in an automated test (not a live submission) — confirmed it POSTs to the exact right endpoint with the right headers, the success message matches spec exactly, a simulated failure shows the right error message with phone/email and re-enables the button, and there are zero console errors. The one real live test (actually hitting Formspree and getting a real email) is still yours to run, same as your own instructions called for.


## Files
- `index.html` (was `website-preview.html`) — homepage
- `gallery.html` (was `gallery-preview.html`) — project gallery
- `privacy.html` — **new**
- `terms.html` — **new**
- `assets/` — logo, favicon, OG image, real job photos, real job video
- Originals backed up before any edits (untouched versions of the two ChatGPT-built files kept separately, not shipped in this folder)

## Media inserted
**Homepage:** hero background, before/after pair (cabinet refinishing), 3 pathway card backgrounds (Residential/Commercial/Repairs), featured video (muted/loop/poster), 6-photo gallery grid, 1 crew-at-work photo in the About section.

**Gallery page:** 6 project cards — commercial drywall, a real before/after pair (bathroom), exterior repaint, featured interior-paint video, a texture/corner detail shot, a second job-site video.

Every piece is a real Patch & Paint Bros photo or video — nothing stock, nothing AI-generated, nothing from another contractor's site. Full list of which job each one came from is in the project's `Website - Best Photos and Video` folder.

## Copy changed
Wording next to each photo/video was written to match what's actually in the shot (per the "media decides the wording" rule) rather than forced to fit the original placeholder captions.

## Bugs fixed (not just media)
- `<footer>` on the homepage was missing its CSS class — the whole footer rendered as unstyled plain text instead of the dark navy footer. Fixed.
- About a third of the homepage had no matching CSS at all: the 3 service cards, the 5-step process, the service-area pills, the "Matters" cards, and gallery.html's entire project grid were unstyled plain text. Built real CSS for all of it.
- 6 separate, conflicting rounds of logo/header CSS overrides (leftover iteration cruft) consolidated into one clean block.
- A duplicate "customer reviews" section saying the same thing twice — removed the redundant one.
- A duplicate Gallery link in the footer — fixed.
- Mobile hamburger menu didn't do anything when clicked — built the real slide-in menu + overlay, works on both pages now.

## Logo
The official logo had a flat white background in every source file — there was no actual transparent version anywhere in the project. Removed the background myself (flood-fill from the edges, not a blind color-key) so it sits directly on the navy header with no white box. Original art, colors, and wording untouched.

## Privacy / legal
- Built `privacy.html` — accurate to what the site actually does: only collects what's typed into the estimate form, no cookies set by the site itself (Google Fonts is the only outside request), no analytics/tracking installed, no third-party data sharing, how to request your info be deleted.
- Built `terms.html` — website-use terms only. Deliberately does **not** invent deposit/cancellation/refund/warranty policies — flagged clearly as "Owner input required" instead (see `OWNER-INPUT-NEEDED.md`).
- Both linked from the footer on every page.
- Added a form-consent line above the estimate form's submit button explaining what happens when it's submitted — no pre-checked marketing opt-in, no auto-subscribe.

## Accessibility
- "Skip to main content" link on every page (keyboard-only users can jump past the header).
- Visible focus outlines added for links, buttons, and form fields (there were none before beyond the form inputs).
- Verified heading hierarchy (one h1 per page, no skipped levels).
- All images have real, descriptive alt text — what's actually in the photo, not keyword-stuffed.
- Icon-only social buttons have `aria-label`s.
- Gallery filter buttons and the mobile menu toggle are real `<button>` elements — keyboard-operable by default.
- Not claiming "ADA compliant" anywhere — built with good practices, not a certified audit.

## SEO / sharing
- Added Open Graph + Twitter card meta tags to both pages (title, description, a built share image using the real logo on navy).
- Added the same LocalBusiness schema to gallery.html that index.html already had (name/phone/email/service area only — no fake ratings, address, or review data).
- Page titles and meta descriptions already existed and were left as-is where accurate.

## Performance
- Oversized source photos (some were 2-6MB straight off a phone camera) resized and compressed to real web dimensions.
- Both videos re-encoded, muted, and set to `playsinline` so they never autoplay sound.
- All below-the-fold images use `loading="lazy"`.

## Remaining placeholders (intentional — mean "still need media")
- None. Every "ADD PHOTO/VIDEO HERE" slot from the original build was filled.

## What's NOT done / needs Sylvia
See `OWNER-INPUT-NEEDED.md` — social URLs, real reviews, the deposit/cancellation policy, domain/hosting status.

## Not claimed
This project does not declare the website "legally compliant" or "ADA compliant." The privacy and terms pages are an honest, accurate starting point, not a substitute for a lawyer's review.

## Update (same day) — Better media, bigger gallery
Per your ask to use better pictures/video and add more to the gallery:
- Added real Downtown Apartment content for the first time — 9 photos (rooms, hallways, a crew-at-work shot) plus the full 49s room-walkthrough video, pulled straight from that job's source files. Same photography flagged earlier as some of the best shot so far.
- Expanded gallery.html from 6 project cards to **18** — pulled additional unused real photos out of every existing job folder (second angles on the bathroom, deck, gray house, great room jobs, etc.) instead of reusing the same single shot per job.
- Swapped the one visibly soft photo (the Teal Townhome exterior siding shot) out for a sharper exterior shot.
- Homepage photo grid grew from 6 to 8, now includes 2 of the new Downtown Apartment shots.

## Update (10/7/26) — Google Analytics + photo quality pass
- Installed Google Analytics (GA4, ID `G-7DB3VY1MFB`) on all four pages; Privacy Policy updated to disclose it with an opt-out link.
- Removed the Commercial Building photo from the homepage grid and gallery (only mid-construction shots exist for that job — see OWNER-INPUT-NEEDED.md); the Commercial pathway card now uses a plain styled background instead.
- Swapped the main **Residential** pathway card photo — was a messy mid-construction shot (debris, tape, exposed seams), now a genuinely finished room (Dark Cabinet Room job, painted walls, natural light, no clutter).
- Flagged other mid-construction photos still in the gallery for a possible follow-up pass (see below) — not swapped yet, pending owner review.
