# Codex AI-DLC Entry Point

This file is the Codex entry point for the AI-DLC workflow.

## Load Workflow
- Load the workflow from `.codex/aidlc-rules/core-workflow.md`.
- Load rule details from `.codex/aidlc-rule-details/`.
- Ignore any legacy rules outside `.codex/` (do not load `.kiro` or `.amazonq` paths).

## Notes
- Follow the workflow exactly as written, including all mandatory logging, question formats, and content validation rules.
- Generate documentation artifacts only under `aidlc-docs/` as required by the workflow.
- Ensure audit logging is written to `aidlc-docs/audit.md` with raw user input and timestamps per the workflow rules.
- When asking questions, use the required multiple-choice format and [Answer]: tag per the question-format guide.

## Default options
- We prefer "User Journey" based user stories.
- For acceptance criteria, we prefer detailed acceptance criteria written using Gherkin syntax.
- For user stories granularity, we prefer Fine-grained stories split into small implementable slices.

## Folder structure

All the project must run inside docker containers using docker compose to orchestrate them.

### Backend (`backend/`)
The backend follows Domain Driven Design (DDD). Important subdirectories include:
- `src/domain` – core entities and domain services.
- `src/application` – application layer with services and orchestrating use cases.
- `src/infrastructure` – persistence adapters (under `persistence/`), security helpers and other integrations.
- `tests` – test projects structured by `api`, `domain`, `infrastructure` and `commands`.

### Frontend (`frontend/`)
The frontend uses Vue and TypeScript, also organised with a DDD mindset within `src/`:
- `domain/` – domain entities, repository interfaces and services.
- `application/` – application use cases.
- `infrastructure/` – concrete implementations and UI (e.g. `api/`, `components/`, `layouts/`, `views/`, `repositories/`, `services/`).
- `tests` – test projects structured by `views`, `services`...

## Programmatic checks

Backend and frontend must use linter to validate the code standards and should have test. The tests should be unit tests and e2e tests. Those checks needs to be configured in the CI and need to be run locally using docker. The frontend should always have a `type-check` script in the package.json to ensure types are being used and enforced. The backend needs to do the same if is built in typescript. If not, needs to use the appropiate command for the used language.

### Frontend
Run these commands from the `frontend` directory:

- `docker compose exec frontend npm test` – execute the frontend test suite.
- `docker compose exec frontend npm run lint` – verify code standards. Many issues can be fixed automatically with `docker compose exec frontend npm run lint-fix`.
- `docker compose exec frontend npm run type-check` – validate TypeScript types.

### Backend
Run these commands from the `backend` directory if backend is done in Typescript. Run the language appropiate command if not:


- `docker compose exec backend npm test` – execute the frontend test suite.
- `docker compose exec backend npm run lint` – verify code standards. Many issues can be fixed automatically with `docker compose exec backend npm run lint-fix`.
- `docker compose exec backend npm run type-check` – validate TypeScript types.

Always run the appropriate checks before committing.

## Architecture rules

- Use cases should not invoke other use cases directly. If common logic needs to be shared, move it into a domain service that both use cases can call.
- The infrastructure layer may reference the infrastructure, application and domain layers.
- The application layer may reference the application and domain layers.
- The domain layer must only reference code from the domain layer.

## Documentation
- The API needs to be documented with Swagger.
