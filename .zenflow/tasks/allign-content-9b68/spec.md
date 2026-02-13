# Technical Specification — Align Content

## Difficulty
Medium — alignment touches multiple sections and breakpoints, using legacy Bootstrap + custom layout rules.

## Technical context
- Static HTML/CSS/JS site.
- Layout relies on Bootstrap grid (`css/bootstrap.min.css`) with custom layout rules in `css/main.css`.
- Page transitions use `.pt-page` / `.section-inner` wrappers and JS (`js/main.js`).
- Primary content lives in `index.html` (sections: `#home`, `#about-me`, `#resume`, `#portfolio`, `#contact`).

## Implementation approach
1. Use Playwright MCP to open the site and navigate each section via the nav links. Capture alignment issues per section at desktop, tablet, and mobile widths.
2. Establish consistent horizontal rhythm:
   - Define a single max content width and center it via `margin: 0 auto`.
   - Normalize left/right padding for `.section-inner`, `.section-title-block`, and `.section-content`.
   - Ensure Bootstrap `.row` gutters align with the content container across sections.
3. Fix section-specific outliers (e.g., sections that have different padding, or elements that overflow the grid).
4. Verify that the start page (`#home`) remains full-width/centered and that custom page transitions are unaffected.

## Source code structure changes
- Update `css/main.css` to introduce consistent alignment rules and section-level overrides where needed.
- If necessary, adjust `index.html` (and any in-scope secondary pages like `portfolio-1.html` or `blog-post-1.html`) to add a shared wrapper class for alignment.

## Data model / API / interface changes
- None.

## Verification approach
- Run a local static server (e.g., `python3 -m http.server`) for Playwright MCP access.
- Use Playwright MCP to check each section at 1440x900, 1024x768, and 375x812:
  - Left edges of headings, copy, and grids align to a shared column.
  - Consistent horizontal padding across sections.
  - No horizontal scroll or clipped content.
  - Navigation and section transitions still work.

## Open questions
- Should alignment fixes apply only to `index.html` sections, or also to standalone pages like `portfolio-1.html` and `blog-post-1.html`?
- Do you want all sections aligned to a centered container, or should any remain full-width (besides the home hero)?
