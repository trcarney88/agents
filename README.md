# OpenCode Agents

This repository contains agent definitions used by OpenCode for software delivery workflows.

## What is here

| File | Type | Purpose |
| --- | --- | --- |
| `engineer.md` | Primary | Lead developer and orchestrator agent |
| `project-planner.md` | Primary | Planning-only agent for project scoping and Obsidian sync |
| `committer.md` | Subagent | Git automation for safe semantic commits |
| `qa.md` | Subagent | Go/TypeScript QA strategy and test execution |
| `reviewer.md` | Subagent | SRP, complexity, readability, and performance review |
| `security.md` | Subagent | Application and infrastructure security auditing |
| `docs_generator.md` | Subagent | Concise inline docs for Go/TS/TSX/Astro |

## Agent roles

- **Primary agents** coordinate work and user interaction.
- **Subagents** are specialized helpers delegated focused tasks.
- Agent files use frontmatter for model, tool access, and permissions.

## Conventions

- Safety constraints deny outbound email sending commands.
- QA and review are split from implementation to encourage verification.
- Commit/push responsibilities are isolated in `committer.md`.
- Planning and implementation are separated (`project-planner.md` vs `engineer.md`).

## Typical workflow

1. Plan work with `project-planner.md` or directly via `engineer.md`.
2. Implement changes through the engineer flow.
3. Validate with `qa.md`.
4. Review with `reviewer.md`.
5. Commit through `committer.md` when approved.

## Notes

- These files are policy/instruction definitions, not application source code.
- Update agent prompts carefully; small wording changes can materially change behavior.

## How to add a new agent

1. Create a new `*.md` file in this directory.
2. Add frontmatter with:
   - `description`
   - `mode` (`primary` or `subagent`)
   - `model`
   - `temperature`
   - `tools` permissions (`read`, `write`, `edit`, `bash`)
   - optional `permission` rules (recommended for safety-sensitive commands)
3. Write a clear mission statement and operating constraints.
4. Define expected workflow steps and output format.
5. Add the file to the table in **What is here**.
6. If it is a subagent, ensure the primary agent docs reference when to delegate to it.

### Checklist for quality

- Scope is explicit (what the agent should and should not do).
- Tool access is minimal and justified.
- Safety/deny rules are present where needed.
- Workflow is deterministic enough to reduce ambiguous behavior.
