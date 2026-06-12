# Agent team

I will use GitHub Copilot CLI in a Codespace to orchestrate this work for Mona's Project Pulse dashboard.

| Agent | Model | Responsibility | Source |
|---|---|---|---|
| Orchestrator | Claude Opus 4.7 | Coordinates the workflow, delegates to specialists, and validates the final result. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 4.7 | Researches the repo, identifies phases, file ownership, dependencies, and validation steps. | `.github/agents/planner.agent.md` |
| Designer | Gemini 3.1 Pro | Defines the dashboard layout, accessibility, information hierarchy, and visual polish. | `.github/agents/designer.agent.md` |
| Coder | GPT-5.5 | Implements the static dashboard files and supporting launch configuration. | `.github/agents/coder.agent.md` |

For Project Pulse, the Orchestrator should involve the Planner first, then split design and implementation work so the Designer can shape the UI while the Coder builds `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json`. The Orchestrator then checks that the pieces fit together into a polished, runnable dashboard.
