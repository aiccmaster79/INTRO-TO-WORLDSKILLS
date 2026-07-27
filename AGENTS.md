# AGENTS.md

## Cursor Cloud specific instructions

This repo is a **single-file static site**: `INDEX.HTML` is a self-contained reveal.js deck
introducing the WorldSkills UK **Digital Support & Security** competition. There is no backend,
package manager, build step, or test suite, and it should stay that way.

### Running it
- Serve the folder over HTTP and open in a browser, e.g. `python3 -m http.server 8081` then
  `http://localhost:8081/INDEX.HTML`. Use HTTP rather than `file://`. Nothing to install or build;
  edit the HTML and refresh.
- **Outbound HTTPS is required at runtime.** reveal.js, highlight.js, Font Awesome and Google Fonts
  load from CDNs (jsdelivr / cdnjs / googleapis). With no network the deck renders unstyled and the
  widgets, which initialise on `Reveal.on('ready')`, never start.

### Design model
The sibling **`PRESENTATIONS`** repo (live at <https://aiccmaster79.github.io/PRESENTATIONS/>) is the
visual and structural model. Reuse its brand palette (`--brand-orange`, `--brand-purple`,
`--brand-teal`), glass cards, `.site-credit` footer, `#circuit-canvas` particle background with
`data-canvas-bg` on the title and closing slides, and its interactive-widget conventions. Its
`PRESENTATION-UPGRADE-PLAN.md` documents the widget library and the per-deck definition of done.

Do not change the brand palette, add build tooling, or add new CDN dependencies.

### What is in the deck
35 slides sourced from the WorldSkills UK Digital Support & Security Technical Handbook 2026, with
speaker notes and a timing cue on every slide (roughly a 90-minute session). Five interactive
widgets — a stage pathway stepper, a competence matrix filtered by stage, a national final timetable
explorer, a scored readiness self-audit, and a rules scenario judge — plus a six-question quiz with a
progress pill, letter grade and retry.

### Widget conventions
- All state lives in the single `AppState` object at the top of the script block.
- Guard every listener with `if (el.dataset.bound) return; el.dataset.bound = 'true';`
- Initialise on `Reveal.on('ready')` and re-initialise on `Reveal.on('slidechanged')`.
- `keyboardCondition` is overridden in `Reveal.initialize` so Space and Enter reach a focused
  control instead of paging the deck. Keep it if you add controls.
- Custom controls rely on the bare `button, input, select, textarea` type rule; form controls do not
  inherit font size, so without it every widget label renders at the browser's 13px default.

### Verifying a change
Open the deck over HTTP and check that:
- the browser console is clean on load and while using every widget;
- the quiz scores correctly and the results grade matches the score;
- no slide overflows its frame at the 1920x1080 authoring size — sections are fixed to `height: 100%`,
  so content that overflows is clipped rather than scrolled, and neither `scrollHeight` nor
  `offsetHeight` will reveal it. Measure the bottom edge of a section's children against its content
  box instead;
- the layout still works at mobile width, and **S** shows the speaker notes.
