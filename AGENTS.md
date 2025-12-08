# Repository Guidelines

## Project Structure & Module Organization
- `START-3/flipbook.php` — WordPress plugin entry point and hooks.
- `START-3/app/` — PHP MVC-style classes: controller, model, view, list-table, helpers.
- `START-3/data/` — static assets for the viewer:
  - `javascript/` (viewer logic; e.g., `BookPreview.js`, various `*.min.js`).
  - `style/` (CSS and icons).
  - `files/` (book pages, thumbs, search data, logo).
- Prefer editing non-minified sources (e.g., `BookPreview.js`) over `*.min.js`.

## Build, Test, and Development Commands
- Local plugin run (recommended): install a WordPress site, then copy or symlink `START-3` to `wp-content/plugins/flipbook`, activate “Flip Book”.
- Quick asset sanity-check: `php -S localhost:8000 -t START-3` (serves assets only; not a full WP runtime).
- No build step is required; assets are committed.

## Coding Style & Naming Conventions
- PHP: use tabs for indentation; follow WordPress-style brace placement. Class names like `FlipBook_*`, methods `lowerCamelCase`.
- JavaScript: 2-space indentation; classes `PascalCase` (e.g., `BookPreviewPublic`), variables `camelCase`; end statements with semicolons.
- Filenames: keep existing names/paths; many files are referenced dynamically by WP and the viewer.
- Do not modify generated `*.min.js/*.min.css` unless necessary; update the readable source and re-minify if you change behavior.

## Testing Guidelines
- Automated tests are not present; use manual smoke tests:
  - Frontend: add `[flipbook id="…"]` to a page; verify toolbar, navigation, search, and media.
  - Admin: create/view/delete books via the Flip Book menu; confirm no PHP warnings.
  - JS changes: check browser console for errors and regressions.

## Commit & Pull Request Guidelines
- Commits: concise, imperative titles; consider a scope prefix (e.g., `php:`, `js:`, `assets:`). Existing history is informal—aim to improve clarity.
- PRs include: summary, rationale, affected paths (e.g., `START-3/app/class-flipbook-model.php:…`), manual test steps, and screenshots/GIFs for UI changes. Note if assets were regenerated.

## Security & Configuration Tips
- Do not commit secrets or site-specific configs. Keep large media under `START-3/data/files/` minimal.
- Sanitize inputs and escape outputs in PHP views; avoid editing search index data unless regenerating it intentionally.

