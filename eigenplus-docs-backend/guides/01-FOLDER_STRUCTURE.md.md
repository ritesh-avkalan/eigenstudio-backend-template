# Folder Structure Guide – eigenplus-backend

This guide explains the structure and responsibility of each folder and file in the `eigenplus-backend` repository. It is designed to help developers navigate the codebase, contribute effectively, and understand where different kinds of logic live.

---
## Root Layout

```
eigenplus-backend/
├── app/                   # Main application code (FastAPI app)
│   ├── main.py            # FastAPI entrypoint
│   ├── models/            # SQLAlchemy ORM models (DB structure)
│   ├── routes/            # All API route definitions
│   ├── core/              # App config, utilities, and DB connection
│   ├── services/          # Business logic and helpers (optional)
│   ├── schemas/           # Pydantic request/response models
│   └── dependencies/      # Common route dependencies (e.g., get_db)
│
├── tests/                 # Unit and integration tests
│   ├── conftest.py        # Fixtures and test config
│   ├── test_files.py      # Example test case file
│
├── .env.example           # Template for environment config
├── requirements.txt       # Python dependencies
├── Dockerfile             # Container build config (optional)
├── alembic.ini            # If migrations are handled locally (optional)
└── README.md              # Project overview and usage guide
```

---

## Folder Breakdown
### `app/`
This is where all the backend logic lives.

- **`main.py`**: Initializes the FastAPI app and includes routers
- **`models/`**: Database tables via SQLAlchemy (mirrors `eigenplus-database` schema)
- **`routes/`**: Each file handles one domain (e.g., `files.py`, `projects.py`)
- **`core/`**: Contains `settings.py` (loads from `.env`) and `db.py` (DB session)
- **`services/`** *(optional)*: Functions that encapsulate reusable logic
- **`schemas/`**: Pydantic models used in requests and responses
- **`dependencies/`**: Shared `Depends()` logic like `get_db()`

### `tests/`
- **Unit tests** for logic, models, and endpoints
- Use `pytest` to run tests
- Includes shared fixtures via `conftest.py`

### `.env.example`
- Define `DATABASE_URL`, `S3_BUCKET`, and other secrets

### `requirements.txt`
- List of packages like `fastapi`, `sqlalchemy`, `pydantic`, `alembic`

---

## Security Guidelines
- Secrets such as database URLs, JWT keys, and AWS credentials must **never** be committed to Git. Only `.env.example` should be committed with placeholder values.
- Use **environment variables** to configure secrets securely in deployment.
- Ensure all API routes with sensitive access are protected with authentication.
- Always validate input using **Pydantic schemas** to prevent injection attacks.
- Limit CORS in production to known frontend domains.
- Use HTTPS and secure cookie settings in production.
- If file uploads are handled, validate file type, size, and store them securely (e.g., in S3 with restricted access).

These measures help prevent unauthorized access, data leakage, and other vulnerabilities as the backend scales.

---

## Best Practices
- Keep each domain (e.g. files, users, jobs) separated in `routes/`, `models/`, and `schemas/`
- Reuse code via `services/` instead of putting logic in routes
- Keep shared DB logic in `core/db.py` and config in `core/settings.py`
- Use `.env` to separate dev/staging/prod environments
- Regularly run tests and linting before pushing code

---

This structure keeps the backend modular, clean, secure, and scalable as your simulation platform grows.