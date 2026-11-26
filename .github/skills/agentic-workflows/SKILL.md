---
name: agentic-workflows
description: Create, compile and repair agentic workflows (gh-aw) for this repository. Use when asked to add an agentic workflow, update an existing one, or regenerate a workflow lock file.
---

# Agentic workflows dispatcher

Agentic workflows are Markdown files in `.github/workflows/` that describe a task for an AI agent.
The `gh aw` CLI compiles each Markdown file into a sibling `.lock.yml` GitHub Actions workflow.

## When to use this skill

- A maintainer asks for a new agentic workflow (for example, a scheduled digest that opens a pull request).
- An existing agentic workflow needs new sources, tools, network access or safe outputs.
- A `.lock.yml` file is missing or out of date.

## Procedure

1. Read the request and write the workflow in `.github/workflows/<name>.md`.
2. Declare sources under `tools:`, permissions under `network:`, and anything that writes back under `safe-outputs:`.
3. Run `gh aw compile <name>` to produce `.github/workflows/<name>.lock.yml`.
4. Commit both the Markdown source and the generated lock file. Never hand-edit a lock file.
5. Trigger the workflow once with `workflow_dispatch` to confirm it starts.

## Rules

- Keep one concern per workflow.
- Never add secrets to the Markdown file; reference `secrets.COPILOT_GITHUB_TOKEN` in the compiled output only.
- Keep `network:` minimal: list only the hosts the workflow actually fetches.
