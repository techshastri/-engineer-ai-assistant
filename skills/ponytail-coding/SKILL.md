---
name: ponytail-coding
description: Use for AI-assisted software development when the user wants minimal, maintainable code; to avoid overengineering; to review changes for bugs, security, tests, and removable complexity; or to install and configure the upstream Ponytail skill for supported coding agents.
---

# Ponytail coding approach

## Source of truth and scope

- Upstream project: https://github.com/DietrichGebert/ponytail
- Read the current README, `INSTALL.md`, `AGENTS.md`, and `skills/ponytail/SKILL.md` before giving version-sensitive installation or behavior guidance. Repository layout and supported clients can change.
- This packaged skill summarizes Ponytail's approach; it is not a vendored copy of the full upstream repository, hooks, commands, tests, adapters, or binaries. Do not claim the user's local coding agent has been modified or that upstream scripts have run.
- Prefer official upstream release/repository instructions. Do not recommend unofficial forks or packages when the official source is available.

## Core decision ladder

Before implementing a feature or refactor, stop at the first adequate option:

1. Is the change needed at all? Avoid speculative features and premature abstractions.
2. Can existing code, components, utilities, or established project patterns solve it?
3. Can the language standard library or native platform capability solve it?
4. Is a dependency already installed that solves it adequately?
5. Can a small, clear implementation solve it without adding a dependency?
6. Only then add the minimum new implementation that satisfies the actual requirements.

Aim for the smallest correct solution, not code golf. Prefer readable, conventional code and the project's existing style. Avoid speculative configuration options, duplicate abstractions, unnecessary wrappers, redundant comments, and dependencies that do not materially improve the result.

## Safety and correctness are not optional

Never remove or weaken:
- input and trust-boundary validation;
- authentication, authorization, escaping, or other security controls;
- meaningful error handling and data-loss protection;
- required tests, especially for risky or boundary-case logic;
- accessibility and user-visible behavior requirements;
- observability needed to diagnose important failures.

For changes involving SQL, credentials, filesystem paths, network access, user data, concurrency, or destructive operations, explicitly inspect edge cases and preserve the relevant safeguards. Keep changes scoped; do not reformat or rewrite unrelated files.

## Implementation workflow

1. Restate the actual requirement and constraints briefly; identify existing behavior that must remain unchanged.
2. Inspect the relevant code and tests before proposing a design. Search for reusable functions and conventions first.
3. Choose the least complex approach that meets requirements; explain any trade-off that materially affects reliability, security, or maintenance.
4. Implement only the necessary changes. Add dependencies only with a clear reason.
5. Test the changed behavior and important failure cases. If tests cannot be run, say so and provide the exact checks that remain.
6. Review the diff for accidental scope expansion, duplicate logic, missing validation, secrets, untested risky branches, and code that can be removed.
7. Summarize changed files, tests run, and any remaining risks. Never claim a command or test succeeded unless it actually ran and its result is known.

## Review and audit requests

When reviewing code, prioritize concrete findings in this order:
1. Correctness bugs and data loss.
2. Security and trust-boundary failures.
3. Missing or inadequate tests for risky logic.
4. Performance and resource issues supported by evidence.
5. Unnecessary complexity or removable code.

For each finding, provide the file/location, impact, reasoning, and smallest practical fix. Distinguish confirmed defects from hypotheses. Do not manufacture issues merely to produce a longer review. For a repository-wide audit, map entry points, data flow, and critical paths before ranking findings by impact and confidence.

## Installing upstream Ponytail

First identify the target coding agent and OS, then follow the current official `INSTALL.md` and README. The repository supports different integration paths for different agents; do not assume one installation command works everywhere. Examples documented upstream have included:

- Claude Code: add the official marketplace `DietrichGebert/ponytail`, then install `ponytail@ponytail`.
- Codex: add the official marketplace and install Ponytail using the current Codex plugin workflow; review/trust lifecycle hooks if the current instructions require it.
- Gemini CLI: install the official extension from `https://github.com/DietrichGebert/ponytail`.
- Other clients: use their matching upstream adapter/rules file or install `skills/ponytail/SKILL.md` as a skill where supported.

Treat these as orientation only; verify exact commands against the current upstream documentation. Review hooks and scripts before authorizing execution. Do not run install commands or modify a project unless the user has asked and an execution-capable tool is available.

## Relationship to OmniRoute

OmniRoute handles model/provider routing; Ponytail shapes how a coding agent approaches implementation. They solve different problems and can be used together, but Ponytail does not itself route model requests and OmniRoute does not automatically install Ponytail's coding rules. If configuring both, handle gateway/provider credentials and coding-agent hooks as separate trust boundaries.
