# Agent Context Kit Quickstart

This guide gets a local knowledge workspace running in a few minutes.

## 1. Install

Release install:

```bash
curl -fsSL https://github.com/tamtnts/agent-context-kit/releases/latest/download/install.sh | sh
```

Windows PowerShell:

```powershell
iwr https://github.com/tamtnts/agent-context-kit/releases/latest/download/install.ps1 -UseBasicParsing | iex
```

Source install:

```bash
git clone https://github.com/tamtnts/agent-context-kit.git ~/agent-context-kit
cd ~/agent-context-kit
pip install -e .
```

## 2. Check The CLI

```bash
agentctx --version
agentctx help
```

If you already have scripts using `contextd`, they can keep using that command name.

## 3. Initialize A Workspace

From the repository root:

```bash
agentctx init
agentctx check
```

`init` creates or confirms `.contextd/config.json`. `check` reports workspace, pack, adapter, and safety status.

## 4. Build A Task Context

```bash
agentctx context "prepare agent context for product requirements" --preview
agentctx explain "prepare agent context for product requirements" --text
```

The first command builds the scoped artifact. The second command explains document selection, dropped docs, gaps, warnings, and source hashes.

## 5. Use It In Another Codebase

Inside the codebase where your agent works:

```bash
agentctx init --knowledge-root ~/agent-context-kit --workspace default
agentctx check
```

Then ask the agent to use the generated context before implementation.

## 6. Connect An MCP Client

```bash
agentctx connect --client codex --knowledge-root ~/agent-context-kit --workspace default
```

Use `--client all` to print snippets for every supported client.

## Common Maintenance Commands

```bash
agentctx find "security policy" --limit 5
agentctx doctor --text
agentctx pack-validate --all --text
agentctx eval --golden --workspace default --text
```