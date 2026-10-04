# AGENTS.md

A convention for coordinating AI coding agents in a collaborative repository, including a ruleset for clean, non-destructive and effective code/repository collaboration and shared workspace management, so that any other human or agent can pick up the agentic work with all the context and information needed to continue from where it was left off, ensuring that agentic workflows happen in a clean, non-destructive and effective way, with all the relevant information and context from agentic runs commited as part of the repository's history.

## How it Works and Why

Instead of agents keeping its own individual memory, agents are instructed to read and write a shared space, making the agentic activity visible and understandable by centralizing agents' activities into a single, standardized and accessible location ([.agents/](.agents/)), mainly **enabling _traceability_ and _accountability_ by having agents' context and activities become part of the repository's history**.

The point is enabling human developers and collaborators to better keep track of whatever AI agents have done, are doing or plan to do, specially the how and why. While the other obvious benefit of that is that it also enables agents the same, so agents can effectively inherit context from truly different sessions, as their memories become actual part of the repository's history.

- **Shared memory.** Agents leave clear indicators for pending work and for data that is outdated, so any agent can pick up where another stopped.
- **Individual memory.** Agent-specific notes go in `.<agent_env_name>/memories/` (e.g. `.claude/memories/`). Anything relevant to other agents must be copied to the shared space.
- **Handoff.** When passing work to another agent, record the context, decisions and pending items in the shared memory.
- **Housekeeping.** Removing or archiving stale memory happens when an agent finds it necessary and the operator approves, or when the operator asks.

### Rules of engagement

Defined in full in [.agents/AGENTS.md](.agents/AGENTS.md). In short:

- Prefer the CLI over MCP when both can do the job.
- Always respect and strictly follow the repository's established workflows, collaboration rules and conventions.
- Never commit, push or touch a remote without being asked.
- Never rewrite `main`; messy history belongs on feature branches, work-trees, etc.
- Clean a branch before merging it.
- Comments explain what the code does and why, not the bug that was fixed.

### Plans

Plans follow [.agents/memories/plan-template.md](.agents/memories/plan-template.md): objective, status, approval, executor, checkbox progress per step, testing strategy and out-of-scope topics.

## Getting started

1. Copy the `.agents/` directory into your repository
4. If desired, fill in the placeholder in [.agents/memories/workflow.md](.agents/memories/workflow.md) and customize as you like
3. If customizing the overall behavior is desired, adapt the rules in `AGENTS.md` as you like
4. Feed it into a test prompt and see how the agent behaves
5. Start a fresh session and make a test prompt without feeding it to see if the agent can pick and follow it on its own
6. If the agent won't read `.agents/` on its own, instruct it (custom initial prompt, private memory file, etc.) to always look out for this directory and its contents when working on a repository.

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
| Plan   | what **to do**  | Discarded* after execution                              |
| Task   | a single action | Discarded* after completion                             |

*Anything worth keeping from a finished plan or task is promoted to a memory and added to the `MEMORY.md` index.
