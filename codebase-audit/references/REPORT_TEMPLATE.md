# Report Template

Use this when producing the final output for `codebase-audit`. Choose the report shape that matches the branch.

## Formal Audit Report

# Codebase Audit Report: [System/Repo Name]

## Executive Summary

- Overall assessment: [healthy / mostly healthy with risks / fragile / high-risk / inconclusive]
- Audit question: [the decision this audit supports]
- Top findings:
  1. [Finding name] — [severity] — [one-line impact]
  2. [Finding name] — [severity] — [one-line impact]
  3. [Finding name] — [severity] — [one-line impact]
- Recommendation: [headline decision or next step]

## Scope and Methodology

- Scope covered: [repos, modules, flows, timebox]
- Scope not covered: [explicit exclusions]
- Access level: [full repo / partial files / snippets / read-only / no runtime]
- Methods used: [manual inspection, scripts, tests, static analysis, sampled flows]
- Commands/tools run: [command + result summary]
- Confidence notes: [where limited access affects conclusions]

## System Map

- Product purpose: [what the system does]
- Stack: [language/framework/runtime/database/etc.]
- Entry points: [files/routes/services/workers]
- Major modules/domains: [brief map]
- Key flows traced: [flow name → major steps]
- Standards observed: [patterns/conventions that seem real]

## Findings

### [Finding Title]

- Category: [Architecture / Organization / Patterns / Tooling / Testing / Security / Docs / DX / Process / Performance]
- Severity: [Critical / High / Medium / Low]
- Effort: [Quick win / Moderate / Major]
- Confidence: [High / Medium / Low]
- Observation: [factual statement]
- Evidence: [file paths, lines, command output, repeated samples]
- Impact: [risk, cost, speed, reliability, onboarding effect]
- Recommendation: [concrete next action]
- Suggested owner: [team/person/role if inferable; otherwise omit]

Repeat for each finding.

## Prioritized Action Plan

| Priority | Action | Severity | Effort | Why now | First step |
|---|---|---:|---:|---|---|
| 1 | [Action] | [Severity] | [Effort] | [Impact] | [Concrete first PR/task] |

## Open Questions

- [Question that needs team context]
- [Question blocked by missing access]

## Appendix

- Sampled files/flows.
- Commands and outputs summarized.
- Dependency/security audit summary.
- Test/build/lint results.
- Docs reviewed.

## Onboarding Scan Report

# Codebase Onboarding Map: [System/Repo Name]

## What This System Does

[Plain-language product/system summary.]

## How to Run, Test, and Build

- Install/setup: [steps or reference]
- Run app: [command]
- Run tests: [command]
- Build/type-check/lint: [commands]
- Known setup gaps: [missing docs, env vars, services]

## Stack and Tooling

- Runtime/language:
- Frameworks:
- Package manager:
- Database/storage:
- CI/CD:
- Testing:
- Lint/format/type-check:

## Mental Model of the Codebase

- Architecture style:
- Major modules:
- Entry points:
- Data flow:
- External integrations:

## Conventions to Follow

- Folder/file placement:
- Naming:
- Error handling:
- State/data access:
- Testing:
- Styling/UI conventions, if relevant:

## A Real Flow Traced

[Flow name]
1. [Step/file]
2. [Step/file]
3. [Step/file]

## Where to Be Careful

- [Risky module or pattern] — [why]
- [Unclear convention] — [what to verify]
- [Missing tests/docs] — [how to compensate]

## Good First Changes

- [Small safe task]
- [Test/documentation improvement]
- [Low-risk refactor aligned to conventions]

## Action Items

| Action | Why it matters | Effort | Suggested first step |
|---|---|---:|---|
| [Action] | [Impact] | [Effort] | [First step] |

## Targeted Audit Report

# Targeted Codebase Audit: [Area]

## Scope

- Area inspected:
- Reason for audit:
- Access limits:

## Local Context

- Related modules:
- Relevant flows:
- Existing patterns this area should follow:

## Findings

Use the same finding shape as the formal audit.

## Recommended Change Plan

1. [Concrete next step]
2. [Follow-up]
3. [Test/doc/tooling update]

## Unknowns

- [What still needs broader repo/team context]

## Finding Writing Rules

A finding is not valid unless it includes:

- Observation: what is true.
- Evidence: where/how it was observed.
- Impact: why it matters.
- Recommendation: what to do next.

Bad finding: “The code is messy.”

Good finding: “Three payment flows validate currency in different layers (`x`, `y`, `z`), which increases the chance of inconsistent billing behavior. Centralize validation behind [module] and add integration tests around mixed-currency payments.”

## Tone Rules

- Be factual and constructive.
- Avoid blame.
- Prefer “the codebase currently relies on…” over “the team failed to…”.
- Use “likely” and “needs confirmation” when evidence is incomplete.
- Do not recommend rewrites unless the evidence shows localized remediation will not address the risk.
