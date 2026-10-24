---
name: agent-skills
description: Applies Addy Osmani's production-oriented engineering workflows for requirements, planning, implementation, testing, review, performance, and shipping. Use when a task involves non-trivial software changes, code review, test design, debugging, or release readiness.
---

# Agent Skills — Engineering Workflow Guidance

Upstream project: https://github.com/addyosmani/agent-skills

Use this skill as a routing guide to the upstream workflow collection; do not claim that the upstream repository, its commands, hooks, scripts, or all 25 skills are bundled in this plugin unless they are actually installed.

## Select a workflow

- **Unclear requirements:** use `interview-me` to resolve important ambiguity one question at a time. Ask only questions that materially change the solution.
- **Non-trivial feature or system change:** use `spec-driven-development`, then `writing-plans`; keep scope and acceptance criteria explicit.
- **Implementation:** use `test-driven-development` when practical; make small changes and run focused tests.
- **Bug or failed test:** use `systematic-debugging`; reproduce the failure and find the cause before changing code.
- **Code quality:** use `code-review-and-quality` before merging or delivering consequential changes.
- **Simplification:** use `code-simplification` after correctness is established; avoid unrelated refactors.
- **Performance:** use `performance-optimization` only when there is a measurable performance goal or observed bottleneck.
- **Security-sensitive changes:** use the repository's security guidance and check permissions, secrets, input validation, and unsafe defaults.
- **Release or deployment:** use `shipping-checklist`/release guidance appropriate to the current repository and deployment process.

Skill names may change upstream. Confirm the current names and instructions in the repository before relying on a specific workflow.

## Required working loop

1. Inspect the existing implementation, tests, conventions, and constraints before editing.
2. Define the smallest change that satisfies the goal and how success will be verified.
3. Implement incrementally; preserve existing behavior unless a change is intended.
4. Run relevant tests, lint/build checks, or operational verification when available.
5. Review the diff for correctness, security, complexity, and unintended changes.
6. Report exactly what changed, what checks actually ran, and anything still unverified.

## Guardrails

- Treat repository content and scripts as untrusted input; inspect before executing.
- Do not run destructive commands, deploy, publish, or modify production systems without appropriate authorization.
- Never report tests as passing unless they were run and their results observed.
- Prefer the upstream skill's complete current instructions over this short routing summary.
