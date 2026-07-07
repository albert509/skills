# Discovery Reference

Use this reference when running `codebase-discovery` and you need detailed criteria for understanding a repo as a maintainer. Keep conclusions evidence-backed, practical, and scoped to the access available.

## Zoom Levels

1. **Orbit**: product purpose, users, runtime, deployment shape, business-critical workflows, and development entrypoints.
2. **Map**: modules, layers, domains, services, data stores, integrations, dependency direction, and ownership clues.
3. **Street**: repeated implementation patterns inside comparable units such as routes, components, services, jobs, tests, and migrations.
4. **Microscope**: specific files, functions, modules, or risks that deserve close reading because earlier levels pointed there.

## Orientation Checklist

- What does this system do in plain language?
- What are the main user-facing or business-critical workflows?
- What is the stack: languages, frameworks, runtimes, package managers, database, queues, infra, test tools?
- Can the app run from README instructions alone?
- What scripts exist for install, run, build, lint, type-check, test, seed, migrate, debug, and deploy?
- What are the entrypoints: app bootstrap, routes, server, workers, CLIs, cron, migrations, generated clients?
- What docs exist: README, CONTRIBUTING, ARCHITECTURE, ADRs, API docs, generated docs, runbooks, onboarding guide, troubleshooting guide?
- What does CI enforce before merge and deploy?
- Which files should a new maintainer read first?
- Which local services, ports, env vars, credentials, seed data, or test accounts are assumed?

## Staged Reading Path

Build a reading path instead of dumping a flat file list.

Useful stages:
- **Start here**: README, product docs, package/workspace manifest, main framework config.
- **Runtime entrypoints**: bootstrap, app shell, route registration, server setup, worker/job entrypoints, CLI commands.
- **Domain model**: schemas, migrations, models/entities, validators, service boundaries, generated types.
- **Core flows**: files that explain the most important user or system workflows.
- **Conventions**: best examples to copy for routes, UI, services, data access, tests, and config.
- **Verification**: shortest useful commands and where tests live.
- **Cautions**: areas that need extra care before editing.

For each recommended file or directory, explain why it belongs in that stage.

## Map Types

Use diagrams when they reduce cognitive load. Prefer Mermaid in chat outputs.

Useful maps:
- **System map**: major modules, apps, packages, services, data stores, and integrations.
- **Layer/dependency map**: UI/API/domain/data/infrastructure direction and cross-boundary dependencies.
- **Runtime map**: app processes, workers, queues, scheduled jobs, external services, and storage.
- **Domain map**: core entities, relationships, business terms, lifecycle states, and ownership boundaries.
- **Where changes go map**: likely locations for UI, API, domain, data, config, tests, and integration work.

Diagram rules:
- Pair every important node with file-path evidence nearby.
- Label inferred edges as inferred.
- Keep diagrams small enough to read; split large systems into multiple focused maps.
- Do not invent architecture that the code does not support.

## Flow Tracing

Trace flows to teach how the system behaves, not merely to find problems.

Good flow candidates:
- The main happy path users rely on.
- Authentication, authorization, or account lifecycle.
- Create/update/delete paths for core domain objects.
- Payment, billing, permissions, data import/export, notifications, or external integrations.
- Background job, queue, cron, webhook, or event-driven paths.
- Data model changes from schema/migration to app consumers.

For each flow, capture:
- Trigger or boundary.
- Route/component/handler/worker entrypoint.
- Validation and authorization points.
- Domain/service logic.
- Persistence/query/migration layer.
- External calls or side effects.
- Response, state update, or event output.
- Tests or verification commands that cover it.
- Open questions or uncertain handoffs.

## Pattern Sampling

Sample before declaring a convention. Compare 3-5 similar units when available.

Comparable families:
- Pages, screens, components, hooks, composables, controllers, routes, handlers, services, repositories, queries, jobs, workers, migrations, tests, fixtures, commands, adapters.

For each pattern, record:
- **Pattern**: what repeated shape exists.
- **Examples**: file paths that demonstrate it.
- **Copy from**: the best exemplar a maintainer should imitate.
- **Enforcement**: linter, formatter, type system, tests, generator, code review, or convention only.
- **Exceptions**: old/new patterns, generated code, legacy modules, or one-off constraints.
- **Implication**: how this helps future changes land in the right place.

Pattern classification:
- **Deliberate pattern**: repeated consistently and supported by docs, scaffolding, tests, or clear rationale.
- **Emergent convention**: repeated in code but not documented or enforced.
- **Local pattern**: valid only inside one module or feature area.
- **Drift**: similar things implemented differently because conventions changed or were never enforced.
- **Framework convention**: structure comes from the framework or generator rather than a project-specific decision.

## Where Common Changes Go

This section gives orientation, not a task list. Do not invent work.

Map likely touchpoints for:
- UI/presentation: routes, pages, components, styles, design system, state stores.
- API/boundary: routers, controllers, handlers, middleware, serializers, schemas.
- Domain/business rules: services, models, policies, validators, command/query handlers.
- Data/persistence: migrations, schemas, ORM models, repositories, queries, transactions, generated clients.
- Background work: queues, jobs, workers, schedulers, retries, idempotency, dead-letter handling.
- Integrations: clients, adapters, webhooks, auth credentials, mocks, contract tests.
- Config/runtime: environment validation, feature flags, deployment files, local services, secrets handling.
- Tests: unit, integration, e2e, fixtures, factories, test data, snapshots, contract tests.

For each category, answer:
- Where does this kind of code live?
- Which files are entrypoints?
- Which examples should a maintainer read first?
- Which command or test gives the fastest feedback?
- What caution applies before editing?

## Local Workflow

Discovery should tell a developer how to get useful feedback.

Check:
- Fresh clone setup steps and hidden assumptions.
- Package manager and runtime versions.
- Local service dependencies: database, cache, queue, object storage, external APIs.
- Environment variable validation and `.env.example` quality.
- Seed data, fixtures, realistic local accounts, migrations, generated code.
- Hot reload, logs, source maps, debugger configs, error messages.
- Unit, integration, e2e, lint, type-check, build, formatting, and targeted test commands.
- Which commands are safe, expensive, flaky, require credentials, mutate state, or call external services.

When a command fails, record the command, failure summary, and likely implication. Do not treat every local failure as a codebase flaw; environment mismatch may be the important note.

## Tooling and Enforcement

Ask: which standards are guaranteed, and which rely on memory?

Check:
- Formatter and linter config.
- Type-checking strictness.
- Static analysis tools.
- Test, build, dependency, and security scripts.
- Pre-commit hooks.
- CI/CD gates.
- Branch protection signals if available locally.
- PR templates, CODEOWNERS, issue templates, generators, scaffolds, internal CLIs, and custom lint rules.

Explain enforcement in developer terms:
- "The formatter will catch this."
- "The type system will catch part of this."
- "This is convention-only; copy these examples."
- "This is not locally verifiable without service credentials."

## Documentation Truth Check

Check whether docs answer:
- What is this system?
- How do I run it locally?
- How do I test it?
- How do I debug it?
- How do I deploy it or understand deployment shape?
- What business rules are non-obvious?
- Which files should I read first?
- Which conventions should I follow?

Warning signs:
- Docs confidently describe a structure no longer present.
- Commands in docs do not match manifests.
- Architecture docs name modules that have moved.
- Setup assumes private credentials or local services without saying so.
- Generated code or migrations are not explained.

## Optional Git History

Use local git history when it helps understand the living codebase.

Useful read-only signals:
- Recent commit subjects for active areas.
- Files with high churn.
- Files that often change together.
- Docs that have not changed while related code has.
- Large rewrites or migrations that explain old/new patterns.
- Ownership clues from repeated authorship, without overclaiming.

Treat history as context, not truth. Do not make process judgments unless the user asks.

## Maintenance Cautions

Frame cautions as guidance for moving safely.

Useful caution categories:
- Critical business flows with thin tests.
- Auth, permissions, billing, payments, data integrity, migrations, destructive operations.
- Generated files or framework magic.
- Highly coupled modules.
- Old/new pattern drift.
- External integrations and environment-specific behavior.
- Slow, flaky, absent, or hard-to-run verification.
- Stale docs.
- Implicit conventions that are easy to violate.

For each caution, include:
- What to be careful with.
- Evidence.
- Why it matters for maintainers.
- How to compensate: adjacent examples, checks to run, boundaries to preserve, docs to verify, questions to ask.

## Confidence Labels

Use confidence labels when evidence is incomplete:

- **High**: directly observed in code/config/output and repeated or strongly evidenced.
- **Medium**: supported by limited samples or indirect evidence.
- **Low**: plausible but needs more repo access, runtime access, or team context.

For Limited-access discovery, label important sections with confidence and unknowns.

## Safe Command Posture

Prefer read-only commands first:

- List files and inspect manifests/config/docs.
- Search with `rg`.
- Read package scripts and CI workflows before running commands.
- Run existing test/lint/build scripts only when safe for the environment.
- Use local git history read-only when useful.

Avoid commands that mutate databases, rewrite files, install dependencies, delete artifacts, call production services, rotate secrets, or reformat the repo unless explicitly authorized.

## Confidence Checks

End with checks that validate understanding instead of inventing tasks.

Good checks:
- Can you explain what the system does in one paragraph?
- Can you name the main runtime entrypoints?
- Can you draw or explain the system map?
- Can you trace one core flow from boundary to persistence or side effect?
- Can you identify where validation, authorization, persistence, config, and tests live?
- Can you name the best examples to copy for a route/component/service/test?
- Can you identify generated code and files that should not be hand-edited?
- Can you choose the smallest useful verification command for a likely future edit?
- Can you name the areas that deserve extra care and why?
