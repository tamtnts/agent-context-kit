# Agent Context Kit Repository Reset Design

## Goal

Publish this codebase as a new independent GitHub repository named `agent-context-kit`, with a clean commit history and safer project-level rebranding away from the original upstream repository.

## Repository Strategy

The GitHub repository will be created as `tamtnts/agent-context-kit`. It will not be a GitHub fork, because GitHub forks preserve upstream commit history and author metadata. The local checkout will be converted into a fresh Git repository before pushing, so the new repository starts from a single clean initial commit.

## Customization Scope

The project will keep its core CLI/runtime behavior intact. Customization will focus on public-facing metadata and documentation: repository name, project description, package metadata, README/quickstart references, release URLs, onboarding links, generated binary/spec names, and visible command examples where changing them is low-risk.

The existing CLI command name may remain compatible where broad renaming would require deeper code changes. Documentation can introduce `agent-context-kit` as the project/repository name while preserving `contextd` as the current command name if required by the implementation.

## Attribution And License

Commit history, upstream remote metadata, and upstream GitHub links will be removed from the new repository. The MIT license file will be preserved, including required copyright/license notice, because removing required legal attribution would be unsafe.

## Verification

Run repository validation that is available locally, prioritizing Python tests or validation scripts. Also verify that no remote points to the original upstream and that the new Git history contains only the fresh commit before pushing.
