# Audit Reference

Use this reference when running `codebase-audit` and you need detailed criteria. Keep conclusions evidence-backed and scoped.

## Zoom levels

1. **Orbit**: product purpose, users, business-critical workflows, deployment/runtime context.
2. **Map**: modules, layers, services, domains, dependencies, boundaries.
3. **Street**: repeated implementation patterns inside comparable units.
4. **Microscope**: specific files, functions, modules, or risks that deserve close reading because earlier levels pointed there.

## Orientation checklist

- Can the app run from README instructions alone?
- Do build, test, lint, and type-check scripts exist?
- Do those scripts pass on a fresh checkout if safe to run?
- What are the entrypoints: app bootstrap, server, routes, workers, CLI, cron, migrations?
- What is the stack: languages, frameworks, package managers, database, queues, infra, test tools?
- What docs exist: README, CONTRIBUTING, ARCHITECTURE, ADRs, API docs, runbooks, wiki?
- What does CI enforce before merge and deploy?
- What do recent commits and PRs suggest about current work, review quality, and churn?

## Architecture and structure

Look for:
- Architectural style: layered/MVC, feature/domain modules, hexagonal, modular monolith, microservices, event-driven, serverless, mixed.
- Consistency between stated architecture and actual code.
- Dependency direction: business rules should not be unnecessarily coupled to frameworks, persistence, or third-party APIs.
- Circular dependencies, cross-boundary imports, shared/global modules that everything depends on.
- Cohesion: code that changes together should live near each other.
- Coupling: unrelated modules should not reach into each other's internals.
- User-flow reality: how many layers/services a normal request actually crosses.

Evidence examples:
- Import/dependency graphs.
- File paths showing boundary crossing.
- A traced flow from request/UI event to persistence/side effect.
- Contradiction between docs and implementation.

## Code organization standards

Look for:
- Organizing principle: technical layer, feature/domain, hybrid, package/workspace boundaries.
- Naming conventions for files, folders, classes, functions, tests, routes, components.
- Placement predictability: whether a new feature has an obvious home.
- Similar-feature variance across 3–5 examples.
- Written conventions versus tribal knowledge.

Finding signals:
- New and old parts use different conventions.
- Similar features arrange files differently.
- Teams rely on imitation without docs or scaffolding.
- Generated files and hand-written files are mixed without clear boundaries.

## Implementation patterns

Look for:
- Recurring patterns: repository, service, controller, factory, dependency injection, composables/hooks, modules, adapters, presenters.
- Whether patterns earn their complexity or are cargo-culted.
- Error handling: swallowed errors, inconsistent throwing/returning, weak user messages, missing logging, no retries/timeouts on external calls.
- Async/concurrency: unhandled promises, race conditions, missing cancellation, no backoff, shared mutable state.
- State/data consistency: competing frontend stores, duplicated server state, transaction boundaries, eventual consistency assumptions.
- Validation and authorization placement.
- Configuration/secrets: centralized, environment-aware, typed/validated, `.env.example`, no hardcoded values.
- Duplication of business logic.
- Complexity hotspots: long functions, high branching, deep nesting, excessive params, large modules.
- Comments that explain why versus comments that restate what.

## Tooling and enforcement

Ask: which standards are guaranteed, and which are only hoped for?

Check:
- Formatter and linter config.
- Type-checking strictness.
- Static analysis/code smell tools.
- Test, build, audit, dependency, and security scripts.
- Pre-commit hooks.
- CI/CD gates.
- Branch protection signals, PR templates, CODEOWNERS.
- Custom scaffolding, generators, internal CLIs, or lint rules that encode team patterns.

Useful evidence:
- Config files and scripts.
- CI workflow files.
- Failing or missing gates.
- Patterns present in code but absent from enforcement.

## Testing strategy

Evaluate both existence and quality.

Check:
- Test pyramid shape: unit, integration, end-to-end.
- Risk alignment: payments, auth, permissions, migrations, billing, data integrity, critical business flows.
- Assertion quality: meaningful behavior versus tautologies or brittle snapshots.
- Flakiness, skipped tests, retries, quarantined suites.
- Speed and developer behavior: whether slow tests make people avoid them.
- Fixtures, factories, seed data, mocks, contract tests.

Coverage is a smoke alarm, not the goal. Pair percentages with representative test reads.

## Dependency, security, and compliance

Check:
- Known vulnerabilities with ecosystem audit tools.
- Dependency freshness and update process: Dependabot/Renovate/manual/emergency-only.
- Deprecated or unmaintained packages.
- Lockfile consistency.
- Secrets in current code and, when available/safe, git history.
- Secrets management approach.
- Input validation, sanitization, parameterized queries, output escaping, auth boundaries.
- License risk for commercial/due-diligence audits.

Never print secret values. Report only type, location, and remediation.

## Documentation gaps

Check whether docs answer:
- What is this system?
- How do I run it locally?
- How do I test it?
- How do I deploy it?
- How do I debug it?
- Who owns which area?
- Why were major decisions made?
- What business rules are non-obvious?

High-value docs:
- README, CONTRIBUTING, ARCHITECTURE, ADRs, OpenAPI/Swagger, generated docs, runbooks, onboarding guide, troubleshooting guide.

Danger signal: docs confidently describe an old version of the system.

## Developer experience

Check:
- Fresh clone to running app: number of steps and hidden assumptions.
- Inner-loop speed: install, build, hot reload, unit tests, integration tests.
- Local data: seed scripts, fixtures, realistic test accounts.
- Debugging: source maps, debugger configs, logs, error messages.
- Discoverability of scripts and common workflows.
- Generated code and migrations workflow.
- Multi-service setup: containers, env vars, local ports, queues, workers.

## Process and Git hygiene

Check:
- Commit message quality and conventions.
- Branch strategy and whether it is followed.
- PR size, review depth, review latency, and merge behavior.
- PR templates, linked issues, test evidence in PRs.
- Issue tracker freshness, duplicates, stale tickets, abandoned roadmap items.
- Hotfix patterns and incident evidence.

## Performance and observability

Use when production behavior matters or data scale is relevant.

Check:
- Logging, metrics, tracing, error tracking.
- Whether alerts are actionable or noisy.
- Known bottlenecks and documented constraints.
- N+1 queries, missing indexes, unbounded queries, large payloads, unnecessary sync work.
- Caching strategy and invalidation.
- Performance budgets, load tests, regression detection.

## Pattern classification

When a pattern appears, classify it carefully:

- **Deliberate pattern**: repeated consistently and supported by docs, scaffolding, tests, or clear rationale.
- **Cargo-culting**: copied pattern whose complexity does not match the local problem.
- **Accidental consistency**: repeated shape likely caused by one author or time period, with no team-level rule.
- **Drift**: similar things implemented differently because conventions changed or were never enforced.

Sampling rule: compare 3–5 comparable examples before naming a pattern or drift.

## Severity

- **Critical**: active risk to data integrity, security, compliance, or production stability. Fix before normal roadmap work.
- **High**: significant delivery drag or real future risk. Plan near-term.
- **Medium**: meaningful friction, occasional bugs, onboarding pain, or maintainability cost. Track and address deliberately.
- **Low**: limited-cost inconsistency or style issue. Fix opportunistically or batch.

## Effort

- **Quick win**: small, low-risk, well-bounded change.
- **Moderate**: needs coordination, tests, or multiple touched areas, but not a re-architecture.
- **Major**: cross-cutting refactor, migration, architecture change, tooling rollout, or team process change.

## Confidence

- **High**: directly observed in code/config/output, repeated or strongly evidenced.
- **Medium**: supported by limited samples or indirect evidence.
- **Low**: plausible concern that needs more access or team context.

## Safe command posture

Prefer read-only commands first:

- List files and inspect manifests/config/docs.
- Run existing test/lint/build scripts only when safe for the environment.
- Avoid commands that mutate databases, rewrite files, install dependencies, delete artifacts, call production services, rotate secrets, or reformat the repo unless explicitly authorized.

When a command fails, record the command, failure summary, and likely implication. Do not treat every local failure as a codebase failure; environment mismatch may be the finding.
