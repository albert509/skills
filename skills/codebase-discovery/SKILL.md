---
name: codebase-discovery
description: Discover, map, understand, and onboard into a software codebase as a professional developer. Use to understand a new or large repo, learn architecture and conventions, trace important flows, identify where common changes happen, prepare to maintain a project, or produce a developer-focused Codebase Field Guide.
disable-model-invocation: true
---

# Codebase Discovery

Use this skill to turn an unfamiliar codebase into a practical working model for a software developer. The goal is not to evaluate the team or create a backlog. The goal is to help the user understand what the project does, how the code is organized, where important behavior lives, which patterns to follow, and how to move safely when they begin maintaining it.

The governing zoom order is **orbit -> map -> street -> microscope**. First understand the product, runtime, structure, and repeated patterns; only then inspect specific files deeply. Do not generalize from one file unless the scope is explicitly local.

## Modes

- **Full discovery**: default mode for "I am new here" or "help me understand this repo." Produce a broad Codebase Field Guide with staged reading path, maps, flows, conventions, local workflow, maintenance cautions, and confidence checks.
- **Change discovery**: use when the user names a feature, bug, module, layer, or workflow they expect to work on. Keep enough global context to avoid local misunderstanding, then deepen the relevant area.
- **Limited-access discovery**: use when only snippets, partial repos, generated listings, docs, or descriptions are available. Label confidence clearly and separate observed facts from likely inferences.

Use [`references/DISCOVERY_REFERENCE.md`](references/DISCOVERY_REFERENCE.md) when you need detailed discovery criteria, map types, pattern sampling guidance, or confidence checks. Use [`references/FIELD_GUIDE_TEMPLATE.md`](references/FIELD_GUIDE_TEMPLATE.md) when writing the final deliverable.

## Non-Negotiables

- **Developer usefulness first**: prefer explanations, maps, reading paths, flow traces, conventions, and "where/how" guidance over abstract critique.
- **Evidence before claims**: support important statements with file paths, line ranges, commands, config values, repeated samples, dependency names, docs, or local git history.
- **Sample before generalizing**: compare 3-5 similar examples before claiming a convention, pattern, or drift.
- **Separate facts from interpretation**: mark hypotheses, missing context, and assumptions explicitly.
- **No invented work**: do not suggest product tasks, backlog items, or code changes unless the user asks for them. Use confidence checks instead.
- **No secret leakage**: if secrets are discovered, state only the location and risk without reproducing secret values.
- **No repo mutations unless asked**: discovery observes and explains. Do not refactor, reformat, create docs, install packages, or modify files unless the user explicitly asks.

## Workflow

### 1. Frame the discovery

Classify the mode, available access, and user goal. If the user did not state a scope, assume Full discovery over the current repository. State what the guide will and will not cover.

Completion criterion: a short scope statement exists with mode, repo/access level, confidence limits, and expected deliverable.

### 2. Orient at orbit level

Find what the system is, who or what it serves, how it runs, and which tools define it.

Inspect, when available:
- README, docs, architecture notes, ADRs, contribution guides, runbooks, and API docs.
- Dependency manifests, lockfiles, workspace/package configs, framework configs, and environment examples.
- Entrypoints: app bootstrap, routing, server setup, jobs, workers, CLIs, cron, migrations, deployment configs.
- Test, lint, type-check, build, seed, migration, and local development scripts.
- CI workflows and local git history when useful and available.

Run only safe commands unless the user gave broader permission. Prefer read-only inspection first. Do not install packages, call external services, mutate databases, or run destructive scripts without permission.

Completion criterion: the notes identify product purpose, stack, run/test/build path, key entrypoints, docs state, tooling surface, and access limits.

### 3. Build the system map

Map the major modules, layers, domains, runtime pieces, data stores, integrations, and dependency directions. Use Mermaid diagrams when they reduce cognitive load, especially for large repos.

Include file-path evidence for each important map node. Avoid diagramming guessed architecture as fact; label uncertain edges.

Completion criterion: the guide can answer "what are the big parts, how do they relate, and where do I start reading?"

### 4. Trace core flows

Trace 2-4 real flows for Full discovery when the codebase is large enough. For Change discovery, trace the target flow plus any supporting flow needed to understand it.

Good flows include:
- UI action -> route/controller -> validation/auth -> service/domain logic -> persistence/side effect -> response.
- API request -> middleware -> handler -> data access -> external integration.
- Background job -> trigger -> worker -> side effects -> retry/error path.
- Data/model change -> migration/schema -> generated types -> consumers -> tests.

Completion criterion: each traced flow lists the major steps, files, handoffs, and checks that prove the trace is real.

### 5. Extract conventions from repeated examples

Sample comparable units before naming a convention: routes, components, services, repositories, tests, jobs, migrations, modules, hooks/composables, commands, or adapters.

For each useful convention, explain:
- What pattern appears to be followed.
- Where examples live.
- Where a future maintainer should copy the pattern from.
- Which parts are enforced by tooling and which rely on imitation.
- Any local drift or exceptions that matter.

Completion criterion: the user knows how to add code in the existing style without guessing from a single file.

### 6. Map where common changes go

Create practical "where/how" guidance without inventing actual work for the user.

Cover relevant change categories:
- UI or presentation changes.
- API, route, controller, or handler changes.
- Domain/business-rule changes.
- Data model, migration, persistence, or query changes.
- Background job, queue, cron, or integration changes.
- Config, environment, deployment, or infrastructure changes.
- Test, fixture, seed, or verification changes.

Completion criterion: the guide explains which directories/files a likely change would touch, what adjacent examples to read, and which checks would build confidence.

### 7. Inspect the local workflow

Determine how a developer gets feedback locally.

Look for:
- Setup/install instructions and hidden prerequisites.
- Run, build, lint, type-check, unit, integration, e2e, seed, migration, and debug commands.
- Fastest useful verification path for common edits.
- Test data, fixtures, local accounts, service dependencies, containers, ports, and env vars.
- Known setup gaps or commands that are present but unsafe to run without context.

Completion criterion: the guide tells a developer how to get oriented locally and which commands are safe or useful for confidence.

### 8. Identify maintenance cautions

Keep judgment developer-centered. Do not inventory defects or rank severity. Explain where to be careful, why, and how to compensate.

Examples:
- Highly coupled or frequently changing areas.
- Generated files, migrations, or framework magic.
- Under-tested critical flows.
- Inconsistent conventions or old/new patterns.
- Auth, permissions, payments, billing, data integrity, external integrations, or destructive operations.
- Docs that appear stale or incomplete.

Use local git history optionally and read-only to identify churn, co-changing files, ownership clues, and doc freshness. Treat history as context, not proof by itself.

Completion criterion: each caution has evidence and practical guidance for moving safely.

### 9. Produce confidence checks

End with checks that help the user assess whether they now understand the codebase. Do not turn these into suggested product tasks.

Good checks ask whether the user can:
- Explain the system in one paragraph.
- Name the main entrypoints and runtime pieces.
- Trace one core flow from boundary to persistence or side effect.
- Identify where validation, authorization, persistence, config, and tests live.
- Find adjacent examples before making a future change.
- Run the smallest useful verification command.
- Name the areas that deserve extra care.

Completion criterion: the checks validate understanding, not task completion.

### 10. Write the field guide

Use one shared Codebase Field Guide shape, with mode-specific emphasis:
- Full discovery fills the guide broadly.
- Change discovery compresses global sections and deepens the target area.
- Limited-access discovery labels confidence and unknowns more aggressively.

Write in a practical maintainer voice. The people who built the system may be in the room, but the user needs enough clarity to work. Attribute rough edges to tradeoffs, drift, missing enforcement, framework constraints, or incomplete evidence.

Completion criterion: the deliverable lets the reader understand the project and navigate future work without needing the raw notes.

## Output Quality Gate

Before finalizing, verify:

- The guide states mode, scope, access limits, and confidence.
- Important claims include evidence.
- Diagrams are used when they reduce cognitive load and are paired with file-path evidence.
- At least one real flow is traced when code access allows it.
- Conventions are sampled from comparable examples.
- Maintenance cautions explain how to move safely, not just what looks risky.
- No product backlog, invented first tasks, or code changes are suggested unless requested.
- Secrets are not reproduced.
- The guide explains the codebase as it is, not how the agent wishes it were.
