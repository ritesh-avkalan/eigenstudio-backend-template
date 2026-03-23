# How to Contribute
Thank you for your interest in contributing to the `eigenplus-backend` project! We welcome bug reports, feature ideas, documentation improvements, and code contributions.

This guide outlines how to get started, coding standards, and how to submit your work.

---
## 1. Setup Instructions
Before you begin, make sure you can run the backend locally:

```bash
git clone https://github.com/eigenstudio/eigenplus-backend.git
cd eigenplus-backend
cp .env.example .env
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

Visit `http://localhost:8000/docs` to confirm it’s working.

---
## 2. Contribution Types
You can contribute in several ways:

- Bug fixes or issue reports
- Feature implementations
- Unit or integration tests
- Improvements to the documentation
- Code cleanups or refactors

---
## 3. Branching & Commit Guidelines
- Fork the repository or create a new feature branch:
  ```bash
  git checkout -b feature/your-feature-name
  ```
- Write clear and concise commit messages:
  - ✅ `feat: add /files POST route`
  - ✅ `fix: prevent duplicate file upload`
- Push your changes and open a pull request
- Reference related issue numbers in your PR description if applicable

---
## 4. Code Style & Linting
We use the following tools:
- `black` for formatting
- `isort` for import ordering
- `mypy` for type checking
- `pytest` for testing

Before submitting a PR, run:
```bash
black .
isort .
mypy .
pytest
```

---
## 5. Testing Changes
All new features should include test coverage. Use the `tests/` directory to add your unit and integration tests.

Run tests with:
```bash
pytest
```

---
## 6. Pull Request Review Process
- PRs should be linked to an issue when possible
- Include a summary of the change and steps to reproduce/test
- One of the maintainers will review and request changes or approve

---
## 7. Community Standards
- Be respectful, inclusive, and patient with other contributors
- Keep discussions focused and constructive
- Submit issues or suggestions via GitHub Issues

---

By contributing to this project, you help build a better, more stable simulation backend and support open collaboration for engineering software.

Thank you!