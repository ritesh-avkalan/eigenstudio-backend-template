# Testing Strategy

This document describes how testing is organized for the `eigenplus-backend` project. It ensures consistent practices across contributors and helps maintain code quality, reliability, and stability.

---
## 1. Why Testing Matters

Testing ensures that:
- Code changes do not break existing functionality
- New features behave as expected
- Bugs are caught early during development
- Refactoring does not introduce regressions

---

## 2. Testing Tools

| Tool       | Purpose                          |
|------------|----------------------------------|
| `pytest`   | Unit and integration tests       |
| `httpx`    | HTTP client for API testing      |
| `black`    | Code formatting                  |
| `isort`    | Import sorting                   |
| `mypy`     | Static type checking             |

---

## 3. Test Structure
Tests are placed inside the `tests/` directory and follow this convention:

```
tests/
├── conftest.py       # Fixtures and test config
├── test_files.py     # File upload/list API tests
├── test_users.py     # (Optional) User endpoints
```

Each test file should match the domain it's testing (e.g., files, users, simulations).

---

## 4. Writing Tests
Tests are written using `pytest` and should follow the `assert` style:

```python
def test_example():
    assert 1 + 1 == 2
```

To test endpoints:
```python
from fastapi.testclient import TestClient
from app.main import app

def test_health_check():
    client = TestClient(app)
    response = client.get("/health")
    assert response.status_code == 200
```

---

## 5. Running Tests
From the project root:
```bash
pytest
```

You can also run with coverage:
```bash
pytest --cov=app
```

---

## 6. When to Write Tests
- Adding a new route or model
- Fixing a bug
- Refactoring any core logic
- Before submitting a pull request

---

## 7. Best Practices
- Write tests as you code, not after
- Isolate logic from I/O so it’s easier to test
- Prefer small, focused test functions
- Use fixtures in `conftest.py` for reusability
- Aim for readable, self-documenting test names

---

## 8. CI Enforcement
All tests are automatically run in GitHub Actions. PRs will not be merged unless the test suite passes.

---

By following this testing strategy, we ensure the backend remains robust, testable, and safe to evolve as the platform grows.