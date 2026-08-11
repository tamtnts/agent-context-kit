# Agent Context Kit

[![CI](https://github.com/tamtnts/agent-context-kit/actions/workflows/ci.yml/badge.svg)](https://github.com/tamtnts/agent-context-kit/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](pyproject.toml)

Build and evaluate reproducible context for AI coding agents.

Agent Context Kit is a local-first toolkit for turning project knowledge into scoped, explainable, and testable context for Codex, Claude, Cursor, and MCP-compatible coding agents.

It is built for developers who want agents to use the right docs, constraints, patterns, runbooks, and workspace rules without loading an entire repository or depending on a hosted memory service.

```text
Project Knowledge
       |
       v
Discovery
       |
       v
Policies / Rules
       |
       v
Context Builder
       |
       v
Scoped Context
       |
       v
Codex / Claude / Cursor / MCP
```

The repository ships the current CLI as `contextd` and also exposes `agentctx` for new installs.

## Why It Exists

AI coding agents work better when they receive a focused context package instead of a pile of unrelated documents. Agent Context Kit gives you a repeatable way to:

- resolve the active workspace for a codebase
- select relevant contracts, patterns, packs, and project notes
- generate a deterministic task context artifact
- explain why each document was selected or dropped
- validate packs, policies, and golden tasks
- connect the same knowledge base to Claude, Codex, Cursor, and MCP clients

## Quick Start

```bash
git clone https://github.com/tamtnts/agent-context-kit.git
cd agent-context-kit
pip install -e .
agentctx init
agentctx check
agentctx context "prepare agent context for product requirements" --preview
agentctx explain "prepare agent context for product requirements" --text
```

`contextd` remains a supported command name:

```bash
contextd check
contextd find "rate limit policy" --limit 5
```

Expected signal: the tool reports the resolved workspace, selected docs, dropped docs, gaps, warnings, and source hashes for the task context.

## Core Workflow

1. Put durable project knowledge in a workspace.
2. Attach stack or workflow packs such as backend API, security, product, QA, or agentic development.
3. Generate task-scoped context for one coding-agent task.
4. Inspect the explain report to see why documents were selected or dropped.
5. Run governance and golden-task checks before trusting the context in real work.

## Repository Layout

```text
agent-context-kit/
  agents/          Shared agent instructions and pipeline rules
  packs/           Stack and workflow knowledge packs
  templates/       Reusable schemas and starter documents
  workspaces/      Workspace-specific source knowledge
  scripts/         CLI, validators, exporters, and MCP adapter
  onboarding/      Static setup guides
```

## Install

From source:

```bash
git clone https://github.com/tamtnts/agent-context-kit.git ~/agent-context-kit
cd ~/agent-context-kit
pip install -e .
agentctx --version
```

Release installers are part of the project structure and are intended for published GitHub releases:

Linux/macOS:

```bash
curl -fsSL https://github.com/tamtnts/agent-context-kit/releases/latest/download/install.sh | sh
```

Windows PowerShell:

```powershell
iwr https://github.com/tamtnts/agent-context-kit/releases/latest/download/install.ps1 -UseBasicParsing | iex
```

## Try The Demo Workspace

```bash
cd ~/agent-context-kit
agentctx init
agentctx check
agentctx context "prepare agent context for product requirements" --preview
agentctx explain "prepare agent context for product requirements" --text
```

## Concepts

- **Workspace**: the knowledge boundary for a team, product, or codebase.
- **Pack**: reusable guidance for a stack or workflow such as frontend, web API, product, security, or QA.
- **Contract**: a rule or schema an agent should follow when producing work.
- **Task context**: a generated artifact containing the focused input for one agent task.
- **Explain report**: a trace showing why the context builder selected or ignored source documents.

## Evaluation

Agent Context Kit includes deterministic checks that can be used to improve context quality over time:

```bash
agentctx doctor --text
agentctx pack-validate --all --text
agentctx policy-check "debug context quality" --text
agentctx eval --golden --workspace default --text
```

The current evaluation layer is local and deterministic. Optional model-assisted evaluation can be added on top for relevance, completeness, compression, and task-outcome scoring without making OpenAI or any hosted model provider a required dependency.

## MCP Adapter

Generate a local MCP configuration snippet:

```bash
agentctx connect --client codex --knowledge-root "$(pwd)" --workspace default
agentctx connect --client all --knowledge-root "$(pwd)" --workspace default
```

## Differentiation

Agent Context Kit focuses on reproducibility and evaluation rather than only "more context":

- deterministic context builds with source hashes
- explainable document selection and dropped-document traces
- policy and pack validation before agent use
- golden-task evaluation for regression testing
- local-first operation with optional AI-assisted quality scoring

## Local-First Model

Agent Context Kit reads local files and writes local artifacts. It does not require an API key, hosted service, remote MCP transport, vector database, or memory database.

## Documentation

- [Build system model](docs/build-system-model.md)
- [Context quality](docs/context-quality.md)
- [MCP adapter](docs/mcp.md)
- [Pack validation](docs/pack-validation.md)
- [Governance](docs/governance.md)
- [Comparison](docs/comparison.md)
- [Evaluation](docs/evaluation.md)
- [Quickstart](QUICKSTART.md)

## License

MIT. See [LICENSE](LICENSE).