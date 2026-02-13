# Technical Specification: Update Personal Website

Difficulty: medium

## Technical context
- Static site with hand-written HTML/CSS/JS (no build tooling).
- Main entry: `index.html`; auxiliary pages: `blog-post-1.html`, `portfolio-1.html`.
- Styling: Bootstrap 3 + template CSS (`css/main.css`, `css/animations.css`, etc.).
- JS: jQuery 2.1.3 with plugins (Owl Carousel, Magnific Popup, Shuffle, Masonry, PageScroll2id, imagesLoaded, validator, Modernizr).
- Contact form backend: `contact_form/contact_form.php` with reCAPTCHA v2 and direct `mail()`.
- Content sources to update from: `Profile.pdf` (LinkedIn export) and `files/CV-Konstantin_Pletenev.pdf`.

## Implementation approach
1. **Content audit + agent.md**
   - Create `agent.md` documenting current site sections (Home, About, Resume, Portfolio, Blog, Contact), the copy to use, and the source for each item (Profile/CV).
   - Extract and normalize latest data: roles (Zencoder, Zing Coach, WANNA, Accenture), summary, achievements, skills, languages, location, phone, email, links.
   - Identify placeholders (blog posts, testimonials, clients) and decide which to update vs. hide.

2. **Content updates (keep look-and-feel)**
   - Update hero titles/subtitles, About/Resume timelines, skills, and achievements to reflect latest CV data.
   - Update contact details (phone, location) and social links.
   - Replace placeholder blog/portfolio entries or mark them as “Coming soon” if no real content is provided.
   - Keep visual layout and typography intact; only minimal CSS tweaks for spacing/legibility if needed.

3. **Refactor/cleanup (KISS)**
   - Fix invalid or inconsistent HTML (e.g., `<lt>` tag, `style="hidden"` usage), add semantic attributes and consistent class names.
   - Add `rel="noopener noreferrer"` to external links with `target="_blank"`.
   - Remove unused scripts (e.g., Google Maps include if map is not rendered) and any dead markup.

4. **Library updates (low-risk)**
   - Update vendor libraries to latest compatible minor/patch releases **without** changing layout (prefer same major versions to avoid large markup changes).
   - Adjust any JS initialization code if a library update requires API changes.

5. **Contact form sanity**
   - Confirm reCAPTCHA keys and desired behavior. If keys are outdated or not needed, disable or remove reCAPTCHA and/or the form.

## Source code structure changes
- Modify:
  - `index.html` (copy updates, timeline edits, contact info, cleanup).
  - `blog-post-1.html` and `portfolio-1.html` (header/footer consistency, placeholder handling).
  - `css/main.css` (minor tweaks only, if required by content length/spacing).
  - `js/main.js` (if library APIs change; remove unused map init).
  - `contact_form/contact_form.php` (recaptcha config or disablement).
- Update vendor assets as needed:
  - `js/*.min.js`, `css/*.css`, and `fonts/` if library upgrades require.
- Add:
  - `agent.md` (site content map and source-of-truth copy list).

## Data model / API / interface changes
- No new data model or API. Existing PHP contact form may be updated for reCAPTCHA configuration only.

## Verification approach
- Manual check (local): open `index.html` in a browser and verify:
  - Navigation works, sections render, carousel/text rotation behaves, portfolio filters work, contact form validation UI still shows.
- Playwright smoke check (optional, if installed):
  - Load `file://.../index.html`, verify key sections exist, and take screenshots for before/after comparison.

## Open questions (need user input)
- Do you want to keep the Blog section (placeholder posts) or remove/replace it?
- Do you want the Testimonials/Clients blocks visible or hidden?
- Should we display personal info like date of birth and marital status on the site?
- Confirm phone number, location, and the preferred “current title” (Head of QA vs. QA Lead vs. Engineering Manager).
- Do you want the contact form active (with reCAPTCHA), or should it be removed/disabled?
