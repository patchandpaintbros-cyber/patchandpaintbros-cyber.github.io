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
- Added Facebook (https://www.facebook.com/profile.php?id=61595272553894) to the homepage: an icon in the top bar next to Instagram/TikTok, and a link in the footer "Follow our work" line.

## Update (10/20/26) — Big content + quality pass (Chris: "better the website... do what is best")
- **New homepage photo (hero):** swapped the soft gray-house shot for a sharp Milton House exterior (finished deep-brown siding, white trim, blue sky). WebP in 720/1152/1920 widths. On phones it's shifted left so more of the house shows. Old hero files are still in assets/.
- **New "Drag to compare" section** on the homepage (after "The details make the difference"): 3 real before/after sliders from the Full House Remodel, same spot, lined up by hand on matching points (chandelier, railing, fireplace). Dining room (drywall repair), Staircase (railing painted white), Brick fireplace (brick painted white, with the note "New flooring by another contractor" so we don't take credit for David's floors). Works with mouse, finger and keyboard. The same 3 sliders are the first 3 cards on gallery.html.
- **"See us in action" video section** now shows 3 videos instead of 1: drywall snap (existing), interior paint snap (new) and Milton primer → finished exterior (new). They only download when someone presses play (preload none), so the page stays fast.
- **Homepage photo grid:** 9 → 12. Added Milton exterior (plays the Milton working video), Full House living room (plays the paint snap) and kitchen built-ins (plays the paint/spray working video, faces blurred).
- **Gallery:** 19 → 29 cards. Added the 3 sliders, the Milton before/after video, the Milton porch photo, the full-house paint split video (with the flooring note), kitchen built-ins, staircase and basement.
- New videos are all 720x1280, silent, web-compressed (2–6 MB each): milton-before-after, milton-working, full-house-paint-snap, full-house-paint-split, full-house-paint-working.
- Tested on a 1440px desktop and a 390px phone: no JS errors, no broken files, no sideways scrolling, and the gallery filter still works.
- NOT done (parked by Chris): rebuilding the older low-res Tia Tita/basement videos (432–540px) from raw footage.

## Update (10/20/26) — Privacy + garage photo
- Removed the customer street address from the basement gallery card ("1807 South 220th Street" → "Omaha metro"). Standing rule from Chris: never show customer addresses on the site; city/area only. Scanned all 4 pages; that was the only one.
- Tia Tita garage photo (homepage grid + gallery) swapped from the odd straight-up gutter shot to a clean side view of the whole garage (`tia-tita-garage-side.jpg`). Skipped the front-facing shot because the customer's license plate was readable.

## Update (10/24/26) — New slogan
- Homepage headline changed from "We repair. We paint. We perfect." to **"Patch it up. Paint it right. Leave it to the Bros."** (Chris's pick, a mix of two options). "the Bros." is kept together so it never leaves "Bros." alone on a line on small phones. Checked at 1440px, 390px and 360px: no sideways scroll.

## Note (10/24/26) — Folder moved
- This website folder now lives at `Documents/Asher Brain/02 - Patch and Paint Bros/Patch and Paint Bros Website` (moved out of Downloads at Chris's request). Nothing on the live site changed.

## Update (10/25/26) — Gallery reorganized by job (Chris: "organize the good jobs... especially the gallery")
- gallery.html: replaced the mixed 29-card grid with **18 job sections**. Each has a header (service · city, job name, one-line description) and that job's photos and videos together (64 tiles total). Filters now show/hide whole jobs; "Exterior Painting" renamed "Exterior & Decks".
- **New jobs on the site:** Modern Exterior Repaint (Omaha), Built-In Cabinets, Gray Craftsman Home (photos + video), Two-Story Deck, Red Deck & Stairs, Backyard Deck, Blair bathroom, Commercial Building, Great Room & Theater, New Build Bedrooms, Vaulted Great Room & Loft.
- **Sharper videos:** Tia Tita (house/garage/dog house), Downtown, basement and others now use the 10/25 HD rebuilds (720x1280 web copies, silent, no ending card, load only when tapped). Old video files kept in assets/video.
- Privacy: commercial video starts after a worker walks out of frame; faces blurred per the TikTok batch. City/area only, no addresses.
- Dark-cabinet photos had baked-in dark bars, cropped out. Slider labels shortened to Before/After so they don't overlap on phones.
- Tested 1440px and 390px: no JS errors, no broken images, no sideways scroll; filter and video lightbox work. Homepage NOT changed.

## Update (10/25/26, later) — Fireplace out, homepage refresh, Repairs fix
- Chris: the brick fireplace looked ugly. Replaced the fireplace before/after slider (homepage "Drag to compare" + gallery) with a **Bedroom drywall repair** slider (Full House pair 12, auto-aligned on the fan/window/ceiling light). Also removed the fireplace living-room tile from the homepage grid. New files: ba-bedroom-drywall-before/after.jpg (900x1200).
- Homepage photo grid (12): added Modern Exterior Repaint, Two-Story Deck, Built-In Cabinets, Red Deck, Gray House; Tia Tita, basement, Downtown and new-construction tiles now play the 10/25 HD videos. Dropped the old deck-staining, cabinet-refinish and second Downtown hallway tiles.
- Chris: "Repairs" should be real repairs. The old "Bathroom Drywall" before/after was actually a garage, so it's now "Garage Drywall" under Drywall. Repairs filter = Full House Remodel + Blair bathroom.
- Retested 1440px / 390px on both pages: no errors, no broken images, no sideways scroll.

## Update (10/25/26, later 2) — No blur, new job names, small towns hidden
- Chris: no blurry photos/videos anywhere. Measured sharpness of every image/video on both pages, then checked the softest at actual size. Removed: Blair bathroom video, hallway repaint video (whole job), Downtown video, great room video + 2 soft great room photos, new-build video, commercial building photos + video (whole job). Homepage Downtown and new-construction tiles are now photos only (no video).
- Removed the Gray Craftsman house from both pages (Chris). Homepage grid 12th tile is now the brown deck.
- Small towns: "McClelland, IA" → "Iowa"; "Blair" → "Nebraska". City only for big areas (Omaha, Bellevue).
- Job names are now customer-facing titles instead of our internal names, e.g. Milton House → "Primer to Chocolate Brown", Full House → "Three Floors, Top to Bottom", Tia Tita → "Every Building on the Lot".
- Fixed a leftover preload of the old gray-house hero image (it downloaded on every visit but wasn't shown); now preloads the Milton hero that's actually used.
- Gallery: 15 jobs / 48 tiles. Homepage grid: 12.
- Blair bathroom job retitled "Small Bathroom, Big Upgrade" (Chris: even a small bathroom or shower can get a new look).

## Update (10/25/26, later 3) — Matched before/afters only (Chris rule)
- Standing rule: every before/after pair must be the same spot and angle (blue board before → same blue area after), best angle available.
- Basement: replaced the mismatched pair with two true pairs: blue board IMG_5767 → IMG_5911 (same yellow box/angle) and narrow room IMG_5783 → IMG_5923. New files basement-blue-*/basement-room-*.
- Garage: before IMG_5636 → after IMG_5709 (same wall, same spot). New files garage-wall-*.
- Built-ins: after now Photo 2 (straight-on, matches the before) instead of the angled shot.
- Modern exterior: no before matched any after angle, so the Before photo was removed; the video shows the real before/during/after.
- Hero note under the headline: "Serving Omaha · Bellevue · Papillion · Surrounding Areas" → "Serving the Omaha Metro" (Chris). Town list kept in Service Areas, FAQ, footer and Google data (local search).

## Update (10/25/26, later 4) — Homepage touch-ups (Chris: "what else needs fixing")
- "The details make the difference" before/after: swapped the letterboxed cabinet photos for the matched, cropped built-ins pair (darkcab-before/after).
- "What can we help with?" cards: old blurry backgrounds replaced. Residential = Bellevue house exterior (pathway-residential-2.webp), Repairs = patched bedroom walls (pathway-repairs-2.webp). Old files kept.
- Removed the empty beige bands around the Preparation/Details/Communication boxes (boxes now outlined, no filled background).
- Footer: removed the duplicate Contact + Quick Links row; kept "Follow our work" (Instagram/TikTok/Facebook).
- "See us in action" interior paint video: now the HD rebuild with the brick fireplace stretch cut (17.2–20.8s) and no ending card (full-house-paint-snap-hd.mp4). TikTok #09 got the same fireplace cut.
