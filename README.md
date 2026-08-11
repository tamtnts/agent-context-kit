# agent-context-kit

Agent Context Kit is a local-first toolkit for turning project knowledge into scoped, auditable context for AI coding agents.

It is built for teams and solo builders who want their agents to use the right docs, constraints, patterns, runbooks, and workspace rules without relying on a hosted memory service or a vector database.

The repository ships the current CLI as `contextd` and also exposes `agentctx` for new installs.

## Why Use It

AI coding agents work better when they receive a focused context package instead of a pile of unrelated documents. Agent Context Kit gives you a repeatable way to:

- resolve the active workspace for a codebase
- select relevant contracts, patterns, packs, and project notes
- generate a deterministic task context artifact
- explain why each document was selected or dropped
- validate packs, policies, and golden tasks
- connect the same knowledge base to Claude, Codex, Cursor, and MCP clients

## Daily Flow

```bash
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

From a release:

```bash
curl -fsSL https://github.com/tamtnts/agent-context-kit/releases/latest/download/install.sh | sh
```

Windows PowerShell:

```powershell
iwr https://github.com/tamtnts/agent-context-kit/releases/latest/download/install.ps1 -UseBasicParsing | iex
```

From source:

```bash
git clone https://github.com/tamtnts/agent-context-kit.git ~/agent-context-kit
cd ~/agent-context-kit
pip install -e .
agentctx --version
```

## Try The Demo Workspace

```bash
cd ~/agent-context-kit
agentctx init
agentctx check
agentctx context "prepare agent context for product requirements" --preview
agentctx explain "prepare agent context for product requirements" --text
```

Expected signal: the tool reports the resolved workspace, selected docs, dropped docs, gaps, warnings, and source hashes for the task context.

## Concepts

- **Workspace**: the knowledge boundary for a team, product, or codebase.
- **Pack**: reusable guidance for a stack or workflow such as frontend, web API, product, security, or QA.
- **Contract**: a rule or schema an agent should follow when producing work.
- **Task context**: a generated artifact containing the focused input for one agent task.
- **Explain report**: a trace showing why the context builder selected or ignored source documents.

## MCP Adapter

Generate a local MCP configuration snippet:

```bash
agentctx connect --client codex --knowledge-root "$(pwd)" --workspace default
agentctx connect --client all --knowledge-root "$(pwd)" --workspace default
```

## Governance Checks

```bash
agentctx doctor --text
agentctx pack-validate --all --text
agentctx policy-check "debug context quality" --text
agentctx eval --golden --workspace default --text
```

## Local-First Model

Agent Context Kit reads local files and writes local artifacts. It does not require an API key, hosted service, remote MCP transport, vector database, or memory database.

## Documentation

- [Build system model](docs/build-system-model.md)
- [Context quality](docs/context-quality.md)
- [MCP adapter](docs/mcp.md)
- [Pack validation](docs/pack-validation.md)
- [Governance](docs/governance.md)
- [Comparison](docs/comparison.md)

## License

MIT. See [LICENSE](LICENSE).