---
name: codebase-audit
description: Use when the user asks to audit, assess, review, health-check, understand, onboard into, map, or produce a report for a software codebase. Also use when another skill needs codebase findings, architectural risks, conventions, onboarding notes, or prioritized engineering action items.
---

# Codebase Audit

A codebase audit is an evidence-first pass through a repository that turns orientation into judgment. The output must help one of two audiences: auditors making technical decisions, or developers learning how to contribute safely in the existing style.

The governing zoom order is **orbit → map → street → microscope**. First understand the product, structure, and repeated patterns; only then judge specific files. Do not promote a finding from a single file unless the scope is explicitly microscopic.

## Branches

- **Formal audit**: produce a decision-grade report with scope, methodology, findings, evidence, risk, and prioritized action plan.
- **Onboarding scan**: produce a contributor-grade map of the system, conventions, common flows, tools, risks, and first-change guidance.
- **Targeted audit**: inspect the requested feature, module, layer, risk, or PR, but gather enough surrounding context to avoid local misjudgment.
- **Limited-access audit**: when only partial files, snippets, or descriptions are available, state the access limits and label conclusions as evidence-backed, likely, or unverified.

Use [`references/AUDIT_REFERENCE.md`](references/AUDIT_REFERENCE.md) when you need the detailed checklist for audit categories, severity, effort, pattern recognition, or evidence examples. Use [`references/REPORT_TEMPLATE.md`](references/REPORT_TEMPLATE.md) when writing the final deliverable.

## Non-negotiables

- **Evidence before verdict**: every finding needs concrete support: file paths, line ranges, command output, config values, dependency names, repeated samples, or documented behavior.
- **Sample before generalizing**: compare 3–5 similar examples before claiming a convention, pattern, or drift.
- **Separate facts from interpretation**: mark hypotheses, missing context, and assumptions explicitly.
- **No taste-as-risk**: style preferences only matter when they create measurable friction, inconsistency, bugs, or onboarding cost.
- **No secret leakage**: if secrets are discovered, report the location and risk without reproducing secret values.
- **No code changes unless asked**: an audit observes and recommends. Do not refactor, reformat, or modify files unless the user explicitly asks.

## Workflow

### 1. Frame the audit

Classify the branch, audience, available access, and audit question. If the user did not state a scope, infer the smallest useful scope from their request and note the assumption.

Completion criterion: a one-paragraph scope statement exists with branch, audience, repo/access level, and what the report will and will not cover.

### 2. Orient at orbit level

Find what the system is, how it runs, and what tools define it.

Inspect, when available:
- README, docs, architecture notes, ADRs, contribution guide, issue/PR templates.
- Dependency manifests and lockfiles.
- Entrypoints, routing, server/bootstrap files, job workers, CLI entrypoints, build configuration.
- Test, lint, type-check, build, and CI scripts.
- Recent commit/PR history if available.

Run only safe commands unless the user gave broader permission. Prefer read-only inspection first. Do not install packages, call external services, mutate databases, or run destructive scripts without permission.

Completion criterion: the audit notes include stack, purpose, run/test/build path, key entrypoints, documentation state, and CI/tooling surface.

### 3. Build the map

Map the major modules, layers, services, domains, and dependency directions. Trace at least one real user-facing or business-critical flow end-to-end when the available code allows it.

Look for:
- Architectural style and whether it is consistently applied.
- Boundary clarity, coupling, cohesion, dependency direction, circular dependencies.
- Mismatch between documented architecture and actual code.
- God modules, shared utilities that became dumping grounds, and cross-boundary reaches.

Completion criterion: the audit contains a concise architecture map, one traced flow, and any structural hypotheses with supporting evidence.

### 4. Read the street-level patterns

Sample repeated units before judging implementation quality. Examples: API endpoints, UI components, data access functions, background jobs, form flows, tests, modules, or service methods.

For each sampled family, compare:
- File/folder placement.
- Naming and organization.
- Error handling.
- State/data consistency approach.
- Validation, authorization, and side-effect handling.
- Test style and coverage of risky behavior.

Completion criterion: each claimed pattern or drift is backed by multiple comparable samples, or explicitly labeled as a local observation.

### 5. Check enforcement and risk surfaces

Assess which standards are guaranteed by tooling and which rely on memory.

Cover the relevant areas:
- Linting, formatting, type checking, static analysis, pre-commit hooks.
- CI/CD gates and branch protection signals.
- Test strategy, test quality, and flaky/slow feedback loops.
- Dependency freshness, known vulnerabilities, licenses when relevant.
- Secrets/configuration handling.
- Documentation accuracy and onboarding completeness.
- Developer experience: setup friction, scripts, local debugging, seed data, error clarity.
- Process hygiene: commits, PR size, review signals, issue tracker state.
- Performance/observability for production or data-heavy systems.

Completion criterion: the audit identifies the enforced standards, unenforced conventions, and highest-risk surfaces that matter to the scope.

### 6. Maintain an evidence ledger

Record potential findings in this shape while inspecting:

- Category
- Observation
- Evidence
- Impact
- Confidence: high, medium, or low
- Severity: critical, high, medium, or low
- Effort: quick win, moderate, or major
- Recommendation

Promote only evidence-backed items into the final findings. Keep weak signals as notes, questions, or follow-up investigation items.

Completion criterion: every final finding has evidence, impact, and a concrete recommendation.

### 7. Prioritize decisions

Sort findings by severity and effort, not by personal preference or discovery order. Put critical/quick-win items first, then high-severity risks, then medium/low improvements. Batch low-value style issues instead of inflating them.

Ask for each finding: what is the actual cost of leaving this as-is for another year?

Completion criterion: the action plan is sequenced and each item has a clear next step.

### 8. Write the deliverable

Use the branch to choose the final shape:

- Formal audit: executive summary, scope/methodology, findings by category, prioritized action plan, appendix.
- Onboarding scan: system map, how to run/test/build, conventions to follow, common flows, risky areas, first safe tasks, open questions.
- Targeted audit: context, inspected path, local findings, surrounding risks, recommended changes, unknowns.

Write constructively. The people who built the system may be in the room. Attribute problems to tradeoffs, drift, missing enforcement, or constraints unless there is direct evidence otherwise.

Completion criterion: the deliverable lets the reader make a decision or start contributing without needing the raw notes.

## Output quality gate

Before finalizing, verify:

- The report states scope and access limits.
- No finding is unsupported by evidence.
- At least one real flow or repeated pattern was sampled when code access allowed it.
- Recommendations are actionable, not just “fix this”.
- Security issues do not expose secrets.
- Onboarding outputs explain how to work with the codebase as it is, not how the agent wishes it were.
