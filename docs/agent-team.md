# Agent team

I will use GitHub Copilot CLI in a Codespace to orchestrate the custom agent team building Mona's Project Pulse dashboard:

| Agent | Target model | Responsibility | Definition |
| --- | --- | --- | --- |
| **Orchestrator** | Claude Opus 4.7 (copilot) | Coordinates the specialist agents, breaks work into phases, assigns explicit file scopes, manages dependencies, and verifies the integrated result. It does not implement the work itself. | `.github/agents/orchestrator.agent.md` |
| **Planner** | Claude Opus 4.7 (copilot) | Researches the repository and relevant documentation, then produces an implementation plan covering steps, file assignments, dependencies, edge cases, risks, and validation. | `.github/agents/planner.agent.md` |
| **Coder** | GPT-5.5 (copilot) | Implements dashboard logic and assigned runnable-app support, following repository patterns with explicit errors, deterministic behavior, and validation. For Project Pulse, this includes `.vscode/launch.json` when assigned. | `.github/agents/coder.agent.md` |
| **Designer** | Gemini 3.1 Pro (copilot) | Defines and implements the Project Pulse UI/UX within its assigned scope, emphasizing accessibility, information hierarchy, responsive behavior, polished project cards, status badges, priority treatment, and clear visual styling. | `.github/agents/designer.agent.md` |

The Orchestrator will have Planner establish the approach first, then delegate implementation and design work to Coder and Designer in parallel where file scopes permit, and integrate and verify the finished dashboard.
