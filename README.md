# AGENTS.md

A convention for coordinating AI coding agents in a collaborative repository through plain Markdown files, including a ruleset for clean, non-destructive and effective code/repository collaboration and shared workspace management. So that any other human or agent can pick up the agentic work with all the context and information needed to continue from where it was left off, ensuring that agentic collaboration is done in a clean, non-destructive and effective way, with all the relevant information and context preserved as part of the repository's history.

## How it works

Instead of agents keeping its own individual memory, agents are instructed to read and write a shared space, ensuring that all relevant information is accessible to everyone involved, specially human developers. The main point is making the agentic work visible and understandable by placing all agents' activities into a single, centralized, easily accessible location under the repository's root ([.agents/](.agents/)), enabling traceability and accountability by having agents' context and activities become part of the repository's history.

The goal is to enable human developers and collaborators to keep track of whatever AI agents have done, are doing or plan to do, including how and why. One clear benefit of this approach is that it also enables agents the same, so agents can also resume context from truly different sessions, as their memories becomes actual parts of the repository's history instead of being isolated on individual developer's environments.

- **Shared memory.** Agents leave clear indicators for pending work and for data that is outdated, so any agent can pick up where another stopped.
- **Individual memory.** Agent-specific notes go in `.<agent_env_name>/memories/` (e.g. `.claude/memories/`). Anything relevant to other agents must be copied to the shared space.
- **Handoff.** When passing work to another agent, record the context, decisions and pending items in the shared memory.
- **Housekeeping.** Removing or archiving stale memory happens when an agent finds it necessary and the operator approves, or when the operator asks.

## Layout

```text
.agents/
├── AGENTS.md              # Working rules and conventions.
├── MEMORY.md              # Index of the shared memory (map only, short summary, no content)
├── memories/<name>.md     # Durable context, one subject per file
├── PLAN.md                # Index of the plans
├── plans/<name>.md        # Plans in progress; removed once executed
├── TASK.md                # Index of the tasks
└── tasks/<name>.md        # Tasks in progress; removed once completed
```

| Kind   | Describes       | Lifecycle                                                |
| ------ | --------------- | -------------------------------------------------------- |
| Memory | what **is**     | Durable; outdated entries are cleaned up in housekeeping |
| Plan   | what **to do**  | Discarded after execution                                |
| Task   | a single action | Discarded after completion                               |

Anything worth keeping from a finished plan or task is promoted to a memory and added to the `MEMORY.md` index.

## Rules of engagement

Defined in full in [.agents/AGENTS.md](.agents/AGENTS.md). In short:

- Prefer the CLI over MCP when both can do the job.
- Always respect and strictly follow the repository's established workflows, collaboration rules and conventions.
- Never commit, push or touch a remote without being asked.
- Never rewrite `main`; messy history belongs on feature branches.
- Clean a branch before merging it.
- Comments explain what the code does and why, never the bug that was fixed.

## Plans

Plans follow [.agents/memories/plan-template.md](.agents/memories/plan-template.md): objective, status, approval, executor, checkbox progress per step, testing strategy and out-of-scope topics.

## Getting started

1. Copy the `.agents/` directory into your repository.
2. Point each agent's instruction file (`CLAUDE.md`, etc.) at `.agents/AGENTS.md` so it is read first.
3. Adapt the rules in `AGENTS.md` to your project.
4. If desired, fill in the placeholder in [.agents/memories/workflow.md](.agents/memories/workflow.md) and customize as you like.
