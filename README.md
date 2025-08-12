# Project Documentation

## Overview
This repository contains a static HTML page built with Bootstrap 5.3, modeled after the official Jumbotron example. There are no JavaScript/TypeScript modules or exported functions in this codebase; all behavior comes from Bootstrap and the theme toggle helper script.

Primary files:
- `index.html`: Main page with a header, jumbotron, two content panels, and a footer
- `confusion`: Duplicate of `index.html` content (HTML document)

External dependencies (referenced by relative paths):
- `../assets/dist/css/bootstrap.min.css` (Bootstrap CSS)
- `../assets/dist/js/bootstrap.bundle.min.js` (Bootstrap JS incl. Popper)
- `../assets/js/color-modes.js` (Bootstrap example script enabling theme toggling)

If these files are not present in your environment, use Bootstrap via CDN (see Examples below).

## Quick start
- Open `index.html` directly in a browser, or serve it locally:
  ```bash
  python3 -m http.server 8000 --directory /workspace
  # Then visit http://localhost:8000/index.html
  ```
- Ensure Bootstrap assets are accessible at the referenced paths, or switch to CDN links.

## Public surface (components and behaviors)
While there are no exported code APIs, the page exposes configurable UI components. You consume and customize them via HTML structure and Bootstrap utility classes.

### 1) Theme Toggle (Light/Dark/Auto)
- Trigger: dropdown button with `id="bd-theme"`
- Behavior: switches document theme using `data-bs-theme` on `<html>`
- Dependencies: `color-modes.js` and Bootstrap JS
- Options: `data-bs-theme-value="light" | "dark" | "auto"`

Minimal markup pattern:
```html
<html lang="en" data-bs-theme="auto">
  <body>
    <div class="dropdown position-fixed bottom-0 end-0 mb-3 me-3 bd-mode-toggle">
      <button class="btn btn-bd-primary dropdown-toggle" id="bd-theme" data-bs-toggle="dropdown">
        <span class="visually-hidden" id="bd-theme-text">Toggle theme</span>
      </button>
      <ul class="dropdown-menu dropdown-menu-end" aria-labelledby="bd-theme-text">
        <li><button type="button" class="dropdown-item" data-bs-theme-value="light">Light</button></li>
        <li><button type="button" class="dropdown-item" data-bs-theme-value="dark">Dark</button></li>
        <li><button type="button" class="dropdown-item active" data-bs-theme-value="auto">Auto</button></li>
      </ul>
    </div>

    <script src="../assets/js/color-modes.js"></script>
    <script src="../assets/dist/js/bootstrap.bundle.min.js"></script>
  </body>
</html>
```

Common customizations:
- Default theme: set `<html data-bs-theme="light">` (or `dark`) instead of `auto`
- Programmatic theme: set `document.documentElement.dataset.bsTheme = 'dark'`

### 2) Jumbotron
- Container: `.p-5.mb-4.bg-body-tertiary.rounded-3`
- Content area: `.container-fluid.py-5`
- Typical children: `h1.display-5.fw-bold`, `p.fs-4`, `.btn.btn-primary.btn-lg`

Usage example:
```html
<div class="p-5 mb-4 bg-body-tertiary rounded-3">
  <div class="container-fluid py-5">
    <h1 class="display-5 fw-bold">Custom jumbotron</h1>
    <p class="col-md-8 fs-4">Lead copy describing the feature or product.</p>
    <button class="btn btn-primary btn-lg" type="button">Get started</button>
  </div>
</div>
```

Common customizations:
- Background variants: swap `bg-body-tertiary` for `bg-dark text-white` or any contextual background
- Width and spacing: adjust padding/margins via Bootstrap spacing utilities (e.g., `p-4`, `my-5`)

### 3) Feature Panels (Two-column section)
- Layout: `.row.align-items-md-stretch > .col-md-6 * 2`
- Panels:
  - Dark panel: `.h-100.p-5.text-bg-dark.rounded-3`
  - Light panel: `.h-100.p-5.bg-body-tertiary.border.rounded-3`

Usage example:
```html
<div class="row align-items-md-stretch">
  <div class="col-md-6">
    <div class="h-100 p-5 text-bg-dark rounded-3">
      <h2>Change the background</h2>
      <p>Use background and text utilities to theme this panel.</p>
      <button class="btn btn-outline-light" type="button">Action</button>
    </div>
  </div>
  <div class="col-md-6">
    <div class="h-100 p-5 bg-body-tertiary border rounded-3">
      <h2>Add borders</h2>
      <p>Add borders and light backgrounds for contrast.</p>
      <button class="btn btn-outline-secondary" type="button">Action</button>
    </div>
  </div>
</div>
```

Common customizations:
- Change grid breakpoints: use `col-lg-6`, `col-sm-12` for responsive behavior
- Buttons: switch to `btn-primary`, `btn-secondary`, `btn-link`, etc.

## Using Bootstrap via CDN (recommended if `../assets` is missing)
Replace the asset tags with CDN links:
```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
...
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```
If you do not need the example theme toggle, omit `color-modes.js`. For theme toggle, use the script from Bootstrap’s examples or implement your own toggling by setting `data-bs-theme`.

## File structure
- `index.html`: main entry page
- `confusion`: duplicate HTML of the jumbotron example (can be removed if unnecessary)

## Accessibility notes
- The theme toggle uses `aria-labelledby` and visually hidden text to aid screen readers
- Buttons include discernible text; ensure your copy remains descriptive
- Maintain sufficient color contrast when customizing background and text utilities

## Known limitations
- Asset paths reference `../assets/...`; update to actual paths or CDN
- No build system or bundler; this is a static page
- No client-side routing; use plain links or add a framework if needed

## FAQ
- How do I change the default theme?
  - Set `<html data-bs-theme="light">` or `dark`. The toggle can still override at runtime.
- How do I add more sections?
  - Copy an existing panel or jumbotron block and adjust classes/content.
- Can I import this into a framework?
  - Yes. Paste the markup into your framework component and ensure Bootstrap CSS/JS are loaded globally or within your app shell.