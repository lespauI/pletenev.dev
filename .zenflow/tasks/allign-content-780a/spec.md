# Technical Specification — align content

## Difficulty
- easy

## Technical context
- Static site composed of HTML, CSS, and vanilla JS with jQuery.
- Styling via `css/main.css` and Bootstrap; behavior via `js/main.js`.
- No build step or framework-specific tooling detected.

## Implementation approach
1. Remove Twitter/Facebook links/icons wherever they appear in page content:
   - Header social links in `index.html`.
   - Portfolio page social buttons in `portfolio-1.html`.
   - Blog page social links and share buttons in `blog-post-1.html`.
2. Hide phone/email and reveal on user action:
   - Replace visible phone/email text with a “Click to reveal” control (button or link) in:
     - About “info-list” on `index.html` (email + phone rows).
     - Contact info blocks on `index.html` (phone + email blocks).
   - Store the real values in `data-` attributes (e.g., `data-label`, `data-value`, `data-href`).
   - Add a small JS handler in `js/main.js` to:
     - Listen for click (and Enter/Space for keyboard users).
     - Swap placeholder text with the real value.
     - Set `href` to `mailto:` / `tel:` when applicable.
     - Add a `revealed` class to prevent re-processing.
   - Add minimal styling in `css/main.css` (if needed) so the reveal control matches existing link styles.

## Source code changes
- `index.html`
  - Remove Twitter/Facebook anchors in `.social-links`.
  - Replace phone/email display with reveal controls in the About info list.
  - Replace contact phone/email text with reveal controls in Contact info blocks.
- `portfolio-1.html`
  - Remove Twitter/Facebook buttons.
- `blog-post-1.html`
  - Remove Twitter/Facebook icons and share buttons.
- `js/main.js`
  - Add click-to-reveal handler (document-ready block).
- `css/main.css`
  - Optional styles for reveal control (cursor, underline, focus state).

## Data model / API / interface changes
- None.

## Verification approach
- Manual:
  - Open `index.html`, `portfolio-1.html`, and `blog-post-1.html` in a browser.
  - Confirm Twitter/Facebook icons/buttons are removed.
  - Verify phone/email show “Click to reveal”, and reveal the correct value on click or Enter.
  - Ensure `mailto:`/`tel:` links are correctly applied after reveal.

## Open questions
- Should Twitter/Facebook be removed only from the header/social icons, or also from blog share buttons and any other occurrences?
- Should the reveal apply to all instances of phone/email across the site (including any future pages), or only the ones in `index.html`?
- Do you want the revealed phone/email to become clickable `tel:`/`mailto:` links after reveal, or just plain text?
