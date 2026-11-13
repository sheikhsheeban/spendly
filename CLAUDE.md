# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Spendly — a personal expense tracker (rupee-denominated) built with Flask + Jinja templates + SQLite, plain CSS, and vanilla JS (no frontend framework or JS libraries). The project is built incrementally as a step-by-step course: placeholder routes and stub files are marked with "Step N" comments indicating where later features (auth, profile, expense CRUD) will be implemented.

## Commands

```bash
# Setup (Windows; venv/ is gitignored)
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt

# Run dev server (debug mode, http://localhost:5001)
python app.py

# Tests (pytest + pytest-flask are installed; no tests/ directory exists yet)
pytest
pytest path/to/test_file.py::test_name
```

## Architecture

- `app.py` — the single Flask app module; all routes live here. Implemented routes render templates (`/`, `/register`, `/login`, `/terms`, `/privacy`). `/logout`, `/profile`, and `/expenses/add|<id>/edit|<id>/delete` are placeholders returning strings, to be implemented in later steps.
- `database/db.py` — currently a stub. Intended contract: `get_db()` (SQLite connection with `row_factory` and foreign keys enabled), `init_db()` (`CREATE TABLE IF NOT EXISTS`), `seed_db()` (dev sample data). The DB file `expense_tracker.db` is gitignored.
- `templates/base.html` — shared layout (navbar, footer, Google Fonts, `style.css`, `main.js`). Pages extend it and fill `title`, `head` (page CSS/inline `<style>`), `content`, and `scripts` blocks.
- `static/css/style.css` — global design tokens on `:root` (`--ink*`, `--paper*`, `--accent`, `--border`, `--font-display`/`--font-body`, `--radius-*`). Reuse these variables for new UI so pages match the site theme. Page-specific styles go in a separate file (e.g. `landing.css`, loaded via the `head` block) or an inline `<style>` in the `head` block (as `terms.html`/`privacy.html` do).
- `static/js/main.js` — global JS, loaded on every page; page-specific JS goes in the template's `scripts` block (e.g. the "See how it works" video modal in `landing.html`).

## Conventions

- Commit messages use an area prefix, e.g. `landing: add privacy policy page`.
- When asked to change one section of a page, keep edits scoped to that section.
