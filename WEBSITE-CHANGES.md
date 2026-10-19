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
- Swapped the site logo for the "Primary Logo" from the official brand-board file (same house/brush/roller mark, no subtitle text or "MM" icon, gold window instead of navy) — cut it out of the brand board, removed its background (first pass used flood-fill and left jagged bite marks in the light drywall-texture area; redone with AI background removal (rembg) for a clean edge), replaced `patch-paint-bros-header-logo.png` directly so every page updates automatically. Added a brand-gold (#B89B5E) outline around the logo per Chris's request, since the logo's navy linework was blending into the navy header/footer — black was tried first and didn't pop enough, gold does. Also rebuilt `og-image.jpg` (social share preview) to match. Favicon already matched the brand board's dedicated icon mark, left as-is.
- Logo redo: Chris was right that the colored outline risked looking like a different logo across different materials — switched to a clean white rounded card behind the (100% unmodified) logo instead, in the header and footer on all 4 pages. privacy.html/terms.html didn't even have a white backing before this — added one there too.
- Hero photo (gray house): confirmed genuinely soft/blurry, not intentional. Checked for sharp alternatives — the rest of that job, Teal Townhome exterior, and most other exterior jobs are also soft. Found sharp exterior shots from the Lawyer Ladies job but all shot at a tilted angle, not a clean hero composition — decided to keep the current photo for now (the hero's dark scrim overlay minimizes how noticeable the softness is) rather than trade blur for bad framing. Revisit if a sharp, well-composed exterior turns up.
- Removed the **Commercial** pathway card from the homepage (and its nav link) — Chris's call, since there's no strong commercial photo/content to back it right now. "Commercial Drywall" stays as a checkbox option on the estimate form since it's still a real offered service. Easy to re-add the card once there's real commercial content.
- New-construction pathway: decided not to split it into its own pathway card — it's folded into Residential, and that card's copy now explicitly says "New construction and existing homes."
- **Big content pass (10/8/26)** — pulled real photos/video from post packs that were never added to the site:
  - Fixed the "proof" before/after cabinet section on the homepage — the after photo was a completely different room (a sliding door) than the before (a built-in cabinet wall). Found the actual matching after-shot of that same cabinet wall (`finished_wall_from_dad.jpeg`, Dark Cabinet Room job) and swapped it in — now a real, matched before/after.
  - Swapped the gallery.html "process" video from generic commercial-building footage to a real basement drywall finish walkthrough (Job 22b, start to finish).
  - Replaced the blurry gray-house exterior photo everywhere it appeared (homepage grid + gallery.html) with a sharp, well-composed exterior from the Tia Tita job (Bellevue).
  - Replaced two mislabeled "finished" photos that were actually mid-construction/unpainted (new-construction and great-room shots) with a genuinely strong finished-looking new-construction shot (coffered ceiling, big windows, Great Room Drywall job).
  - Replaced the Blair bathroom photo (every photo from that job turned out to be unpainted blueboard, not actually finished) with real Basement Drywall Finish content instead.
  - Added Basement Drywall Finish to the gallery for the first time — a labeled before/after pair plus a standalone finished shot — and added it to the homepage grid too.
  - Added real Tia Tita exterior content (main house, garage, and a smaller structure) to both the homepage grid and gallery.html for more real variety, per Chris's "use everything we've built" ask.
  - Homepage photo grid grew from 7 to 9 photos; gallery.html grew from 16 to 19 cards.
  - Swapped the homepage's big "SEE US IN ACTION / Real job-site footage. Not stock." video from the Studio Paint Finish clip to the full Tia Tita Main House walkthrough — hadn't been used anywhere on the site yet, bigger and more comprehensive showcase.
  - Added a click-to-play-video feature: any photo with a matching real job video (marked with a play icon) now opens a lightbox and plays it — Tia Tita main house/garage/doghouse, the basement before/after pair, and one downtown hallway shot, on both the homepage grid and the gallery page. Click outside, the X, or Escape closes it.
  - Rebuilt the **Residential** and **Repairs** pathway card photos as real half-before/half-after splits instead of single photos — Residential uses the Dark Cabinet Room wall (same exact spot, primed → painted dark), Repairs uses the existing matched bathroom repair pair.

## Update (10/18/26), Chris's review pass
- Removed the phone number from the top header next to "Free Estimate" (it's still in the hero button, contact section, footer, and mobile call bar).
- Swapped the "Real job-site footage" video from the Tia Tita exterior walkthrough to the new Full House Remodel finger-snap before/after (pro-edited, 23s, compressed to 3MB, 720x1280), with new caption text and poster.
- "Built around quality" photo: replaced the crew-at-work shot with an edited, finished main-floor drywall photo (Full House Remodel).
- Gallery footer logo: removed the screen-blend and brightness filter that washed it out. Kept it transparent (no white card, per Chris), full logo with height:auto and object-fit:contain so it isn't cut off. Gallery phone number untouched.
- Homepage footer logo: also made transparent to match the gallery (no white card).

## Update (10/18/26), "Professional Upgrade" zip (applied partially)
Chris dropped in `Patch-and-Paint-Bros-PROFESSIONAL-UPGRADE.zip` (built outside this project on top of the current files). Applied:
- Hero description rewritten: drywall finishing, repairs, texture matching, interior/exterior painting, Omaha + surrounding metro.
- Estimate form: autofill hints (name/phone/email/ZIP), numeric keypad for ZIP, 16px inputs (stops iPhone zoom-in), bigger full-width submit button on phones, "No obligation to hire" helper line, styled success/error message box.
- "How it works" intro line reworded; gold top border on the 5 process steps.
- Mobile hero sizing/button wrap tweaks; reduced-motion support on both pages.
Skipped:
- The drag before/after slider on the cabinet proof photos. The two photos are framed completely differently (the before has black letterbox bars and a wider crop), so overlaying them would look broken. The zip's own README said to keep side-by-side in that case. Kept the existing side-by-side.
Note: the zip's README claimed gallery lazy-loading was added. It wasn't. The only gallery change was reduced-motion CSS.
privacy.html/terms.html in the zip were identical to the current ones.

## Update (10/18/26), website checklist pass
- Tested every page on iPhone 15, iPhone SE, Pixel 7, iPad, laptop, desktop Safari and a 1920px monitor: no broken images, no JS errors, no sideways scrolling (after the fix below).
- Fixed: on small phones (iPhone SE size) the gallery header's MENU button stuck out 5px, so the page wiggled sideways. Logo shrinks a little under 380px wide now.
- Fixed: the phone Call / Text / Estimate bottom bar existed in the HTML but had never been styled, so it was always hidden (the page even reserved space for it). It's now a navy bar with a gold Estimate button on phones. The gold "FREE ESTIMATE" side tab is hidden on phones because it was covering form text and the submit button; it still shows on tablets and computers.
- Estimate form: sent a live test (labeled TEST) and it arrived in patchandpaintbros@gmail.com. Gmail put it under the Updates tab. Added a hidden `_subject` so form emails now say "New Free Estimate Request - PPB Website" instead of "New submission from A New Form".
- Every link and file (57 unique URLs) checked live: all load. The only failure is patchandpaintbros.com/..., which is expected until the domain is connected.
- Speed: phones on 4G took about 5.3s to show the hero photo. Changes: the header and footer logo now use a lossless WebP copy (`patch-paint-bros-header-logo.webp`, pixel-identical to the PNG, 172KB instead of 274KB; the original PNG is still in assets/). The hero photo now loads first (fetchpriority). The cabinet before/after photos and the footer logo now load lazily.
- Fixed the TikTok link typo (@paintandpatchbros → @patchandpaintbros). Chris confirmed every account is patchandpaintbros.

## Update (10/18/26) — Domain connected
- Chris changed the GoDaddy DNS for patchandpaintbros.com: 4 A records for @ pointing at GitHub Pages (185.199.108-111.153), replacing the "WebsiteBuilder Site" coming-soon page, and the www CNAME pointing at patchandpaintbros-cyber.github.io. The other records (pay, _domainconnect, _dmarc, NS, SOA) were left alone.
- GitHub Pages custom domain set to patchandpaintbros.com. A `CNAME` file was added to this folder so publishes keep it.

## Update (10/18/26) — Phone speed pass
- Hero photo now served as WebP in two sizes (720w 20KB / 1152w 37KB, was a 112KB JPG). The browser picks the right one per screen.
- Residential/Repairs pathway card photos are WebP at 720w (29KB + 15KB, were 158KB + 142KB JPGs).
- Header logo has a 320w WebP option (18KB) for small or low-density screens. Sharp phone screens still get the full-size logo.
- Text-jump fix: added size-matched fallback fonts ("Playfair Fallback" from Georgia, "Montserrat Fallback" from Arial), so the headline doesn't shift when the Google fonts finish loading.
- Original JPGs and the PNG logo are still in assets/ and untouched.

## Update (10/18/26) — Phone header layout + menu bug
- Menu bug: on phones, tapping ☰ turned the screen grey and nothing could be tapped. The dark backdrop (`.nav-scrim`, z-index 55, outside the header) was stacking above the menu panel (inside the header's z-index 50 context). Moved the backdrop to z-index 49 so it sits behind the header and menu. Menu links work now. Tapping outside the menu still closes it.
- Per Chris: on phones and tablets the header is now ☰ + Free Estimate on the LEFT and the logo on the RIGHT. The menu slides in from the left. The ☰ turns into ✕ while it's open. Gallery's "MENU" text button became ☰ to match, and the gallery got a Free Estimate header button too (phones/tablets only). Computer layout is unchanged (logo left, links right).
- Removed an old 220px minimum width on the logo box for phones; it made the page scroll sideways once the logo moved right.
