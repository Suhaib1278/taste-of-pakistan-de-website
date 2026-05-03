---
trigger: always_on
description: Guidelines and architectural patterns used within the SovereignVPN codebase.
---

# Core Engineering Standards (The Standard)

These coding standards define a high-performance, type-safe architecture. Maintaining these conventions ensures a modular, scalable codebase and prevents architectural drift.

## 1. General Philosophy
- **Simplicity & Directness:** Prefer raw, readable logic over abstractions or heavy frameworks unless absolutely necessary. The project favors clear, procedural implementation.
- **Privacy First:** Never log sensitive information (e.g., raw recovery keys, plain-text API keys, IP addresses outside of what's strictly necessary).
- **Security:** Ensure data at rest is encrypted (e.g., VPS API Keys using Fernet encryption in `database.py`). Recovery keys must be hashed (SHA-256) before database insertion.
- **Greenfield Integrity:** For new projects, the **Manager Pattern** and **FastAPI** structure are mandatory from the first commit. Do not use temporary "script-style" files for core logic.

## 2. Backend (Python/FastAPI)
- **Framework & Routing:** Use strictly FastAPI. Define endpoints cleanly in `main.py` using Pydantic models for request bodies.
- **Modularity (Manager Pattern):** Group feature-specific logic into `Manager` classes.
  - Examples: `DatabaseManager`, `MoneroManager`, `RedisManager`, `ServerManager`.
  - Avoid putting heavy business logic directly inside API route handlers.
- **Dependency Map:** Use FastAPI's `Depends()` for repeated auth headers or contexts, specifically `get_current_session`, which checks Redis.
- **Database (SQLite):**
  - Use `sqlite3` driver directly. Do not introduce heavy ORMs (like SQLAlchemy or Alembic) unless fundamentally refactoring.
  - Handle lightweight schema migrations directly in `_init_db()` using `PRAGMA table_info`.
- **Logging:** Do not use `print()`. Always use the configured RAM-only logger (`import logging; logger = logging.getLogger(__name__)`).
- **Cryptographic Keys:**
  - Leverage `secrets` module over `random` for any security-bound random generation (like `generate_recovery_key()`).
- **Type Safety:** All Python functions MUST include type hints (e.g., `def get_user(id: int) -> User:`) to ensure data integrity.
- **Pydantic Schemas:** Every API endpoint must have a `response_model` defined in the decorator. Do not return raw dictionaries from routes.
- **Context-First:** Before using `file_write`, you MUST `file_read` or `ls -R` to verify the current code state. Never "hallucinate" the existence of a function or variable.

## 3. Frontend (Vanilla Web)
- **Minimalist Stack:** Continue using vanilla HTML, CSS, and JavaScript. Avoid pulling in React/Vue/Svelte or heavy bundlers like Webpack, unless the project complexity drastically increases.
- **Single Page Feel:** Interactivity should be driven by lightweight vanilla DOM manipulation within `index.html`.
- **Progressive Web App (PWA):** maintain functionality via `sw.js` and `manifest.json`. Ensure offline caching routes remain correct.
- **State Management:** Interactivity must be driven by a global `appState` object. Do not store application logic inside DOM element attributes (e.g., avoid `data-status="active"` for logic checks).
- **Security:** Use `textContent` instead of `innerHTML` when rendering user-supplied data to prevent XSS.

## 4. Error Handling
- Throw `HTTPException` early in FastAPI routes for validation errors or unauthorized attempts.
- Return explicit `{"status": "error", "message": "..."}` JSON dictionaries where appropriate rather than empty 500s.
- Log caught backend exceptions clearly (`logger.error(f"Error action: {e}")`).