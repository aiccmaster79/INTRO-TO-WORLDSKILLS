# AGENTS.md

## Cursor Cloud specific instructions

This repo currently contains a single, **empty placeholder** `INDEX.HTML` — there is no real content,
backend, package manager, build step, or test suite yet.

### Running it
- Serve the folder over HTTP and open in a browser, e.g. `python3 -m http.server 8081` then
  `http://localhost:8081/INDEX.HTML`. Nothing to install or build; edit HTML and refresh.

### Design model
This site is intended to be built out as a "WorldSkills intro" using the sibling **`PRESENTATIONS`**
repo as the visual and structural model. When adding content, mirror that repo's approach: a static
reveal.js deck / catalog, its brand palette and chrome, and its interactive-widget patterns. Keep it
a dependency-free static site (styling/JS via the same CDNs `PRESENTATIONS` already uses — reveal.js,
highlight.js, Font Awesome, Google Fonts), so outbound HTTPS is required at runtime once CDN assets
are added. The `Technical-Handbook-Digital-Support-Security-2026` is the source reference for the
intro's content.
