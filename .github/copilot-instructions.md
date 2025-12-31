# Copilot instructions — Waiz Hussain portfolio

This repository is a small static single-page portfolio. The goal of this file is to give AI coding agents the exact, discoverable knowledge needed to make safe, useful edits quickly.

1) Big picture
- Single-page static site: `index.html` (markup), `script.js` (behavior), `styles.css` (presentation). No build tools, no server. Edit files directly and preview by opening `index.html` in a browser.

2) Key files & responsibilities
- `index.html`: page structure. Sections are identified by `id` attributes (e.g. `#home`, `#about`, `#projects`) — those ids are relied on by the JS scrolling and active-link logic.
- `script.js`: DOM behavior. Important selectors and behaviors:
  - Mobile menu: `.hamburger` toggles `.nav-menu` and `.hamburger` classes.
  - Smooth scroll: uses `a[href^="#"]` and computes `target.offsetTop - 60`.
  - IntersectionObserver: used for fade-in animations on `section` and `.project-card` elements. Observer options are defined near the top (`threshold: 0.1`, `rootMargin: '0px 0px -50px 0px'`).
  - Active nav highlighting: uses `section[id]` offsets and matches links in `.nav-menu a`.
- `styles.css`: uses CSS variables in `:root` (e.g. `--primary-color`, `--accent-color`). Responsive rules for 768px and 480px breakpoints; several class names (listed below) are tied to JS behavior and must not be renamed without updating JS.

3) Immutable selectors / class names (do not rename unless you update both places)
- `.hamburger`, `.nav-menu`, `.navbar`, `.project-card`, `.nav-menu a`, `section[id]`.

4) How to add a new section correctly (example)
- Add a new `<section id="faq">...</section>` to `index.html`.
- Add an anchor to the nav: `<li><a href="#faq">FAQ</a></li>`.
- Ensure styles for the section follow existing patterns and that `script.js` will observe it automatically (it selects all `section`).

5) Small edits that commonly require touching multiple files
- Renaming a nav id or class: update `index.html` and search `script.js` for selectors (or vice versa). Example: changing `#projects` requires updating the anchor href and nothing else only if you keep class names the same.
- Changing animation timing or the observer threshold: edit the observerOptions in `script.js` and, if needed, the CSS `transition`/`animation` durations in `styles.css`.

6) Developer workflow
- Preview: open `index.html` in a browser. No `npm`, no build step.
- Commit pattern: small projects here use straightforward commits (e.g. `chore: add copilot instructions`, `fix: correct nav selector`).
- Deploy: pushing to `main` and enabling GitHub Pages (branch: `main`, root: repository) is the expected path for publishing.

7) Debugging tips
- If a section does not animate, confirm it is not `display:none` and that `observer.observe(section)` runs (check console for JS errors).
- If nav links do not highlight, inspect computed `offsetTop` values and the `-100` / `-60` offsets used in the scroll/active logic.

8) Safety & quick guardrails for the AI
- Avoid adding heavy frameworks or introducing a build system without explicit instruction — this repository intentionally contains only static assets.
- When changing class names/IDs, always run a repo-wide search and update `script.js` and `styles.css` accordingly.

9) References (files to inspect for examples)
- `index.html` — page layout and nav anchors.
- `script.js` — event handlers, IntersectionObserver, smooth scroll.
- `styles.css` — variables, breakpoints, visual patterns.

If anything here is unclear or you want the instructions expanded (examples for adding a component, CI steps, or a small test harness), tell me which area to expand and I'll update this file.
