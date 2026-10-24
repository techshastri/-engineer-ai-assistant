---
name: chatgpt-mem
description: Use when the user wants to add, configure, understand, or troubleshoot persistent memory across AI coding/chat sessions using zhanyong-wan/chatgpt-mem.
---

# ChatGPT Mem integration guidance

## Upstream source of truth

- Repository: https://github.com/zhanyong-wan/chatgpt-mem
- Read the current README, installation instructions, supported platforms, and license before recommending commands or claiming compatibility. Do not assume the repository name means it integrates directly into ChatGPT's hosted memory or this plugin.
- This skill is guidance only. It does not bundle or execute the upstream repository, install its dependencies, access the user's conversation archive, or create persistent memory on its own.

## First determine the intended memory layer

Clarify or infer whether the user wants: (1) project/repository memory for a coding agent, (2) personal cross-session conversation recall, or (3) memory shared across multiple agents. Explain that these are different scopes and that a local repository memory tool does not automatically read ChatGPT account history or modify ChatGPT's built-in memory.

## Safe setup workflow

1. Inspect the upstream README and recent releases for the current requirements, supported OS/agents, installation method, storage location, and data flow.
2. Identify the user's OS, target agent, and whether memory must stay local or may use a hosted/model backend.
3. Prefer the smallest supported installation path; use a virtual environment or isolated package manager where the project supports it.
4. Before indexing/importing history, inspect included paths and exclusions. Exclude credentials, `.env` files, tokens, private keys, and unrelated personal/company data.
5. Explain whether content is stored locally, transmitted to a model/API, or synced to a remote service based on verified upstream documentation. Do not promise local-only privacy without evidence.
6. Make a backup before importing, migrating, or rewriting memory stores. Do not delete or overwrite existing memory without explicit approval.
7. Verify installation with the documented version/doctor/status command and test one small, non-sensitive memory write followed by retrieval. Report what was actually verified.

## How it complements this assistant

- OmniRoute concerns model/provider routing and gateway operations.
- Ponytail encourages minimal, maintainable, safe code changes.
- Graphify maps project artifacts and relationships into a queryable knowledge graph.
- ChatGPT Mem concerns persistent memory/retrieval as implemented by its own upstream project.

These are separate tools; adding this skill does not wire them together automatically. Integrate them only through documented interfaces and keep secrets, permissions, and storage boundaries separate. If Graphify is used to map the memory project's source, exclude the live memory database and secret/config files unless explicitly required.

## Troubleshooting

1. Confirm repository version and documented prerequisites.
2. Check that the expected memory store exists and is writable without exposing its contents.
3. Check exclusions and whether the intended agent actually invokes the memory retrieval step.
4. Run the project's documented diagnostics and inspect sanitized errors.
5. Test retrieval with a distinctive, non-sensitive phrase known to be stored.
6. Avoid broad filesystem indexing, credential uploads, disabling security controls, or destructive cleanup as first-line fixes.

## Response style

Give concise, verified instructions with upstream links. Distinguish project-provided behavior from this plugin's guidance. Never claim memory was imported, saved, synchronized, or made available to ChatGPT unless the user or a connected tool confirms it.
