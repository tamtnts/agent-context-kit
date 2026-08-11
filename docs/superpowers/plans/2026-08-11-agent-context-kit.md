# Agent Context Kit Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish the cloned source as `tamtnts/agent-context-kit` with a clean history and project-level rebranding.

**Architecture:** Treat this as a repository reset and metadata/documentation customization, not a rewrite of the CLI engine. Keep runtime internals stable while changing public repository identity and release links.

**Tech Stack:** Git, GitHub CLI, PowerShell, Python 3.10+ project metadata in `pyproject.toml`, Markdown documentation.

## Global Constraints

- New GitHub repo name: `agent-context-kit`.
- Preserve required MIT license notice.
- Do not push a GitHub fork that preserves upstream history.
- Remove upstream remote and replace it with `https://github.com/tamtnts/agent-context-kit.git`.
- Keep CLI/runtime behavior intact unless a rename is clearly safe.

---

### Task 1: Repository Identity Cleanup

**Files:**
- Modify: `pyproject.toml`
- Modify: `README.md`
- Modify: `QUICKSTART.md`
- Modify: `contextd.spec`
- Modify: `release/install.sh`
- Modify: `release/install.ps1`
- Modify: `onboarding/index.html`
- Modify: `onboarding/index.en.html`
- Modify: `onboarding/install.html`
- Modify: `onboarding/install.en.html`

**Interfaces:**
- Consumes: Existing project metadata and docs.
- Produces: Public repository identity as `agent-context-kit` while preserving current command compatibility.

- [ ] **Step 1: Scan upstream naming**

Run: `rg -n "github.com/[^ ]*/legacy-context-engine|legacy-context-engine releases" .`

Expected: list of docs, release scripts, and metadata containing upstream naming.

- [ ] **Step 2: Update public-facing metadata**

Use structured edits where possible and direct Markdown/HTML edits where needed:

```text
Project name: agent-context-kit
GitHub repo: tamtnts/agent-context-kit
Short description: Build system for AI coding-agent context kits.
CLI compatibility note: the current executable remains contextd.
```

- [ ] **Step 3: Verify metadata references**

Run: `rg -n "github.com/[^ ]*/legacy-context-engine|legacy-context-engine clone" .`

Expected: no matches outside preserved legal/license context.

### Task 2: Fresh Git History And GitHub Repo

**Files:**
- Modify: `.git` repository metadata only.

**Interfaces:**
- Consumes: Customized working tree from Task 1.
- Produces: Fresh local Git repository with one initial commit and new GitHub remote.

- [ ] **Step 1: Remove old Git history safely**

Run in PowerShell after confirming the resolved path is `C:\Users\ADMIN\contextd\.git`:

```powershell
$repo = Resolve-Path C:\Users\ADMIN\contextd
$gitDir = Resolve-Path C:\Users\ADMIN\contextd\.git
if ($gitDir.Path -ne (Join-Path $repo.Path ".git")) { throw "Unexpected git dir: $($gitDir.Path)" }
Remove-Item -LiteralPath $gitDir.Path -Recurse -Force
```

Expected: `.git` directory removed from the cloned source.

- [ ] **Step 2: Initialize clean repository**

Run:

```bash
git init
git branch -M main
git add .
git commit -m "Initial agent context kit import"
```

Expected: one local commit on `main`.

- [ ] **Step 3: Create GitHub repository**

Run:

```bash
gh repo create tamtnts/agent-context-kit --public --source . --remote origin --push
```

Expected: remote repository exists and initial commit is pushed.

### Task 3: Verification

**Files:**
- Read: repository status and tests only.

**Interfaces:**
- Consumes: Fresh pushed repository.
- Produces: Evidence that history, remote, and validation are acceptable.

- [ ] **Step 1: Run local validation**

Run the available validation command:

```bash
python -m pytest scripts
```

If pytest is unavailable, run:

```bash
python scripts/validate.py
```

Expected: tests or validation complete, or a clear missing-dependency note.

- [ ] **Step 2: Verify Git state**

Run:

```bash
git log --oneline --decorate --all
git remote -v
git status --short
```

Expected: one local commit, origin points to `tamtnts/agent-context-kit`, and no uncommitted changes.
