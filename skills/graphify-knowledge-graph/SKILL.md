---
name: graphify-knowledge-graph
description: Use when the user wants to map, understand, query, document, or navigate a codebase and its docs, SQL schemas, configs, PDFs, or other supported project artifacts with Graphify.
---

# Graphify codebase knowledge graphs

## Upstream source and scope

- Official repository: https://github.com/Graphify-Labs/graphify
- Official package: `graphifyy` (the CLI command is `graphify`). Do not confuse it with similarly named packages.
- Before giving version-sensitive instructions, check the current upstream README, `INSTALL.md`, release notes, and platform-specific guidance. The supported platforms and commands evolve.
- This packaged skill explains how to use Graphify; it is not a vendored copy of the complete repository. It does not install or execute the CLI, bundle its Python dependencies, or install hooks on the user's machine. Do not claim that a graph has been built unless the user or an execution tool confirms it.

## What Graphify does

Graphify builds a queryable knowledge graph from a project. It can map code relationships (such as imports, calls, inheritance, and subsystem communities) and, depending on installed extras and extraction mode, connect code with documentation, SQL schemas, configuration, PDFs, images, and other supported media. It emits artifacts such as `graphify-out/graph.json`, `GRAPH_REPORT.md`, and `graph.html` when those outputs are enabled.

Its code-only AST extraction is designed to run locally without an LLM backend. Semantic extraction for non-code documents/media may call the configured assistant/backend; clearly explain this privacy boundary and recommend `--code-only` when the user wants to limit processing to code. Do not promise that all input types are always processed locally.

## Recommended setup

1. Identify OS, target coding agent, project size, and whether the user needs code-only or document/media extraction.
2. Verify prerequisites against the current upstream README. The documented general prerequisites include Python 3.10+ and `uv` (recommended) or `pipx`.
3. Prefer the isolated official install:
   - `uv tool install graphifyy`
   - or `pipx install graphifyy`
4. Register the skill for the correct agent using the documented command. `graphify install` is the general entry point; current docs may require an explicit `--platform` for Codex, Cursor, Gemini, Copilot, or other clients. On PowerShell, use `graphify .` / the documented CLI form rather than assuming a slash-prefixed slash command works in a shell.
5. Run `graphify --help` and `graphify --version` to verify the actual installation, then build a graph for the intended project folder.
6. Inspect generated output and query it before installing automatic hooks. Confirm exclusions and data scope before indexing private repositories or documents.

Use the current upstream documentation for extras such as SQL, PDF/Office, cloud model backends, Neo4j/FalkorDB, or MCP. Install only the extras the user actually needs. Do not assume optional features are present in the base package.

## Useful workflow

Build or refresh a graph using the current documented command for the selected version. Typical patterns from upstream include:

- Build the current project: `graphify .`
- Refresh changed content: `graphify . --update`
- Skip visualization: `graphify . --no-viz`
- Extract code only: `graphify extract . --code-only`
- Query: `graphify query "what connects authentication to the database?"`
- Trace a path: `graphify path "ComponentA" "ComponentB"`
- Explain a node: `graphify explain "ComponentName"`

Treat these as orientation, not a guarantee that flags are unchanged; check `graphify --help` and the current upstream README. For PowerShell, shell syntax and command names can differ from agent slash commands.

## Querying and interpreting results

- Start with a scoped question, then use `graphify query`, `path`, or `explain` rather than reading the entire graph/report for every question.
- Use `GRAPH_REPORT.md` for a broad architecture overview and `graph.html` for interactive exploration when generated.
- Distinguish source-explicit `EXTRACTED` relationships from `INFERRED` or ambiguous relationships. Inferences are useful leads, not proof; validate important claims in the original source files.
- For an architecture or bug investigation, trace relevant entry points and dependencies, inspect the connected source, then test any proposed change.
- Update the graph after branch changes, pulls, merges, or relevant documentation edits as directed by current upstream guidance. Hooks are optional; don't install them without explaining their effects.

## Privacy, security, and operations

- Code-only parsing is local by design, but semantic passes over docs/media can send content to the configured model/backend. Verify which files are included and which backend is used before processing confidential material.
- Respect `.gitignore` and configure `.graphifyignore` for secrets, generated files, large data, or sensitive corpora. Never index credential files unnecessarily.
- For shared HTTP MCP serving, keep loopback binding by default. If a team needs remote access, require authentication, TLS/reverse-proxy controls, firewall restrictions, and a protected API key. Do not recommend exposing an unauthenticated service publicly.
- Inspect hook scripts and target paths before installing hooks. Avoid overwriting user config or running destructive cleanup. Use the documented uninstall command; only purge generated graph data with explicit user approval.
- If results are incomplete, check ignored files, parser/extras availability, graph freshness, and extraction logs before assuming the graph is accurate.

## Response style

Prefer the smallest useful workflow. Explain which commands are verified against current upstream docs and which are examples. Never claim installation, indexing, tests, or MCP startup succeeded unless actually confirmed. Link to the official repository when current behavior needs verification.

## How it fits the other skills in this plugin

- OmniRoute routes model/provider requests.
- Ponytail guides minimal, maintainable implementation decisions.
- Graphify maps project structure and relationships so the coding agent can reason over a codebase.

These tools complement each other but do not automatically install or run one another. Keep their configuration, permissions, hooks, credentials, and data-processing boundaries separate.
