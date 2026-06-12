# Agent team

This repository uses a small custom agent team to build Mona's Project Pulse dashboard. Work is orchestrated using the GitHub Copilot CLI in a Codespace.

- Orchestrator — Gemini 3.1 Pro (copilot)
  - Coordinates Planner, Coder, and Designer; breaks work into phases, delegates tasks, and verifies integration.
  - Definition: .github/agents/orchestrator.agent.md

- Planner — GPT-5.4 mini (copilot)
  - Researches the codebase, produces implementation steps, file assignments, dependencies, validation criteria, and open questions.
  - Definition: .github/agents/planner.agent.md

- Coder — GPT-5.4 mini (copilot)
  - Implements code, fixes bugs, produces runnable app support (e.g., .vscode/launch.json) within the Orchestrator-assigned file scope, and validates changes.
  - Definition: .github/agents/coder.agent.md

- Designer — Claude Haiku 4.5 (copilot)
  - Handles UI/UX, accessibility, information architecture, and polished dashboard styling (CSS hooks and responsive layout).
  - Definition: .github/agents/designer.agent.md

Note: Agents' internal rules instruct them not to stage/commit/push; repository changes are managed through the Copilot CLI workflow.
