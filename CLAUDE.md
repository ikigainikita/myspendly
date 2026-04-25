# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Spendly** is a Flask-based personal expense tracking web application using SQLite. The app follows a multi-step curriculum where `database/db.py` contains scaffold comments indicating what students implement as they progress.

## Architecture
EXPENSE_TRACKER/
├── static/              # Static assets (CSS, JS, Images)
│   ├── css/
│   │   └── style.css    # Global stylesheet
│   └── js/              # Client-side scripts
├── templates/           # HTML Jinja2 templates
│   ├── base.html        # Main layout wrapper
│   ├── landing.html     # Homepage/Landing page
│   ├── login.html       # User login page
│   ├── privacy.html     # Privacy policy
│   ├── register.html    # User registration
│   └── terms.html       # Terms and conditions
├── database/            # Database files or migration scripts
├── venv/                # Python virtual environment (ignored by git)
├── .gitignore           # Specifies files for Git to ignore
├── app.py               # Main FastAPI/Flask application entry point
└── requirements.txt     # List of Python dependencies
## where things belongs
new routes - "app.py" only, no blueprints
DB logic - database/db.py only 
new pages- new ".html" file extending "base.html
page specific style- new ".css" file , not inline <style> tags 
## code style
1. Use a modular structure: separate Routes (app.py), Logic (logic/), and Models (database/).
2. Follow PEP 8 standards for Python and use semantic classes in HTML/CSS.
3. Keep routes "thin" by delegating complex calculations and DB queries to external modules.
4. Implement Template Inheritance using base.html to avoid redundant HTML code.
5. Prioritize external stylesheets in static/css/ over inline styles for better maintainability. 
## tech constraints 
Framework: Use Flask exclusively for routing and server-side logic.

Database: Use SQLite for data storage to keep the project portable and serverless.

Frontend: Use Vanilla JavaScript only; no external libraries like React or Vue.

Styling: Use Custom CSS in static/css/; avoid CSS frameworks like Bootstrap or Tailwind.

Dependencies: Strictly use the current requirements.txt; no new pip packages allowed.
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
## warnings and things to avoid 
Dependency Lockdown: NEVER install or suggest new pip packages; stick strictly to the existing requirements.txt.

Logic Separation: NEVER put database queries or complex business logic directly inside route functions in app.py.

Frontend Purity: NEVER use JavaScript frameworks (React, Vue, etc.) or CSS frameworks; stick to Vanilla JS and Custom CSS only.

Database Integrity: SQLite foreign key (FK) enforcement is manual; ensure PRAGMA foreign_keys = ON; is executed on every connection.

Route Standards: NEVER use raw string returns for stub routes; always return a proper TemplateResponse or a valid redirect.


