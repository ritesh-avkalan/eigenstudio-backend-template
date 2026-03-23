# EigenStudio Backend Template

This template is the shared starting point for backend services we build at EigenStudio. It organizes API code, domain models, content, project documentation, and tests in a consistent structure so new services begin with the same foundation.

## Folder Structure

```text
.
├── app
│   ├── api
│   ├── core
│   ├── credentials
│   ├── dependencies
│   ├── models
│   ├── schemas
│   ├── services
│   └── utils
├── content
│   └── Solid_Mechanics
│       └── 02_stress_at_a_point
├── eigenplus-docs-backend
│   ├── changelog
│   ├── guides
│   ├── roadmap
│   └── templates
└── tests
    └── integration
```

## What Each Folder Is For

- `app`: Main backend application package.
- `app/api`: Route handlers, endpoint registration, and API-facing modules.
- `app/core`: Core configuration, settings, startup logic, and shared backend foundations.
- `app/credentials`: Local credential helpers, auth configuration, or secret-loading interfaces.
- `app/dependencies`: Shared dependency injection helpers and request-scoped dependencies.
- `app/models`: Internal domain models and persistence-layer models.
- `app/schemas`: Request and response schemas, DTOs, and validation shapes.
- `app/services`: Business logic and service-layer orchestration.
- `app/utils`: Small shared helpers and utilities.
- `content`: Structured domain content used by the backend.
- `content/Solid_Mechanics/02_stress_at_a_point`: Example subject-area content hierarchy for educational or domain-specific data.
- `eigenplus-docs-backend`: Internal backend project documentation.
- `eigenplus-docs-backend/changelog`: Release notes and backend change history.
- `eigenplus-docs-backend/guides`: Setup guides, contributor notes, and operational references.
- `eigenplus-docs-backend/roadmap`: Milestones, planning, and backlog direction.
- `eigenplus-docs-backend/templates`: Reusable documentation templates for specs and planning.
- `tests`: Automated test suites.
- `tests/integration`: Integration tests that verify behavior across modules or external boundaries.

## Working Conventions

- Keep transport concerns in `app/api` and business logic in `app/services`.
- Put shared validation contracts in `app/schemas` and internal data representations in `app/models`.
- Use `app/core` for settings and application-wide bootstrapping, not feature-specific logic.
- Store project planning and operational documentation in `eigenplus-docs-backend` instead of mixing it into application code.
- Empty template folders include `.gitkeep` so the structure is preserved in Git.

## Notes

- This repository already includes existing documentation files inside `eigenplus-docs-backend`; the template structure above describes the main folders teams should keep consistent.
- Update this README whenever the backend template evolves so future services inherit the same conventions.
