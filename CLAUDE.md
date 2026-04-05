# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Spendly** is a Flask-based personal expense tracking web application using SQLite. The app follows a multi-step curriculum where `database/db.py` contains scaffold comments indicating what students implement as they progress.

## Commands

```bash
# Install dependencies (already in venv)
pip install -r requirements.txt

# Run the app (port 5001, debug mode)
python app.py

# Run tests
pytest

# Run a single test file
pytest tests/test_file.py -v
```

## Architecture

```
app.py              # Flask app entry point + all routes
database/db.py      # SQLite helpers: get_db(), init_db(), seed_db() (student-implemented)
templates/          # Jinja2 HTML templates (base.html extends layout)
static/css/style.css # Design system via CSS variables
static/js/main.js    # Client-side JS
```

- `app.py` defines routes directly — no blueprints. Routes render templates but do not yet have backend logic (auth, session, database).
- `database/db.py` is intentionally empty scaffold. Functions to implement: `get_db()` (SQLite connection with row_factory + foreign keys), `init_db()` (CREATE TABLE IF NOT EXISTS), `seed_db()` (sample data).
- The `base.html` template provides the navbar, footer, fonts (DM Serif Display, DM Sans), and CSS variable-based design system. All pages extend it via `{% extends "base.html" %}`.
- CSS variables: `--accent: #1a472a` (deep green), `--accent-2: #c17f24` (amber), `--ink: #0f0f0f`, `--paper: #f7f6f3`.

## Current State

Routes defined in `app.py`:
- `/` → landing page
- `/register`, `/login` → auth pages (templates exist, no backend logic)
- `/terms`, `/privacy` → legal pages
- `/logout`, `/profile`, `/expenses/add`, `/expenses/<id>/edit`, `/expenses/<id>/delete` → placeholder returns ("coming in Step X")
