# Continuous Integration Guide

This document outlines the Continuous Integration (CI) process for the `eigenplus-backend` project. CI ensures code quality, prevents regressions, and maintains a stable main branch through automated checks and tests.

---
## 1. Overview
The CI workflow is powered by **GitHub Actions**. It runs automatically on every pull request and push to the `main` branch.

The CI pipeline performs:
- Code formatting check with `black`
- Import ordering check with `isort`
- Type checking with `mypy`
- Unit tests with `pytest`

---
## 2. Workflow File
CI is defined in `.github/workflows/ci.yml`:

```yaml
name: Backend CI

on:
  push:
    branches: [main]
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    - uses: actions/setup-python@v4
      with:
        python-version: '3.11'

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Check formatting
      run: black --check .

    - name: Check imports
      run: isort . --check-only

    - name: Type checking
      run: mypy .

    - name: Run tests
      run: pytest
```

---

## 3. How to Run Locally Before Pushing
Run the following locally to catch issues before committing:

```bash
black .
isort .
mypy .
pytest
```

You can optionally add a pre-commit hook using [pre-commit](https://pre-commit.com/) to automate these.

---
## 4. Fixing CI Failures
- **Formatting issue?** Run `black .` and commit the changes.
- **Import issue?** Run `isort .`
- **Type issue?** Check `mypy` output and update annotations.
- **Test failure?** Run `pytest -s` locally and debug the failing test.

---
## 5. Benefits
- Catch issues early
- Enforce consistent style
- Prevent broken code from being merged
- Maintain confidence in each deployment

---

All contributors are encouraged to keep CI passing before submitting PRs. This ensures a stable and healthy backend service.