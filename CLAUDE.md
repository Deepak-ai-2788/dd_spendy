# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

- **Install dependencies**: `pip install -r requirements.txt`
- **Run the application**: `python app.py` (access at http://127.0.0.1:5001)
- **Run tests**: `pytest` (tests will be discovered in the project; currently no test files exist)
- **Initialize the database**: The database schema and seed data should be implemented in `database/db.py`. Once implemented, you can initialize by running a script or calling the functions from a Python shell.

## Project Structure

```
expense-tracker/
├── app.py                  # Main Flask application with route definitions
├── requirements.txt        # Python dependencies (Flask, Werkzeug, pytest, pytest-flask)
├── database/
│   ├── __init__.py         # Package initializer
│   └── db.py               # Database functions (get_db, init_db, seed_db) - to be implemented
├── static/
│   ├── css/style.css       # Custom CSS with design tokens and component styles
│   └── main.js             # JavaScript placeholder (currently empty)
└── templates/
    ├── base.html           # Base template with navbar, footer, and CSS/JS imports
    ├── landing.html        # Home page with hero, features, and CTA sections
    ├── login.html          # Login form with error handling
    └── register.html       # Registration form (similar to login)
```

## Architecture Overview

This is a Flask web application for personal expense tracking. The application follows a conventional Flask structure:

- **Routing**: All routes are defined in `app.py` using Flask decorators. The routes include authentication endpoints (login, register) and placeholder routes for expense management (logout, profile, add/edit/delete expenses).
- **Templates**: HTML templates use Jinja2 templating and inherit from `base.html`. The base template includes a sticky navigation bar, main content area, and footer.
- **Static Assets**: Custom CSS defines the design system (colors, typography, spacing, and component styles). The CSS uses CSS variables for easy theming. JavaScript is currently a placeholder.
- **Data Layer**: The `database` module is intended to handle SQLite database connections and operations. The `db.py` file should contain:
  - `get_db()`: Returns a SQLite connection with row factory and foreign keys enabled
  - `init_db()`: Creates tables using `CREATE TABLE IF NOT EXISTS`
  - `seed_db()`: Inserts sample data for development
- **Configuration**: The application runs in debug mode on port 5001. Environment variables or configuration files are not currently used but could be added for production settings.

## Key Files to Modify

1. **database/db.py**: Implement the database functions to set up and interact with the SQLite database.
2. **app.py**: Replace placeholder route implementations with actual functionality that interacts with the database.
3. **templates/**: Extend or modify HTML templates as needed for new features (e.g., expense listing, forms).
4. **static/css/style.css**: Adjust design tokens or add new component styles if required.
5. **static/js/main.js**: Add interactivity for frontend features.

## Testing Approach

Tests can be written using pytest and pytest-flask. A typical test structure might include:
- `tests/conftest.py`: Fixtures for the Flask app and database
- `tests/test_auth.py`: Tests for login, registration, and logout
- `tests/test_expenses.py`: Tests for expense CRUD operations

Run tests with `pytest` from the project root.

## Notes

- The application uses SQLite for simplicity; the database file will be created at `expense_tracker.db` in the project root (as per `.gitignore`).
- CSS uses a custom design system with variables defined in `:root`. Modifying these variables will change the theme.
- The base template includes Google Fonts (DM Serif Display and DM Sans) preconnect links for performance.
