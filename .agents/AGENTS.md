# Agents in a Multi-Agent System for the Project

This document outlines the roles, responsibilities, and interactions of agents within the multi-agent system for the Project.

## Global Memory Space

```text
.agents/MEMORY.md              # Current Context, Overview, Collective Memory Summary
.agents/memories/<memory>.md   # Specific Memory Files
```

The global memory space must serve as the centralized information repository for the multiple agents in this multi-agent system. It should allow agents to access and update shared data, such as task status, environmental observations, and inter-agent communications, facilitating context-retrieval, coordination and collaboration. By using this common memory space instead of the default individual and private memory spaces, agents can efficiently exchange knowledge, track the state of the environment and the running or pending tasks and plans, so that no bit of information is lost when the user engages with different agents.

It is then the responsibility of all agents to ensure that they leave clear indicators for any data that may be relevant for future operations, such as pending tasks, planning, and operations. Additionally, agents must also provide clear indicators for any data that becomes no longer needed or outdated, so that it is well known that it can be safely removed or archived when needed to free up memory resources and maintain the efficiency, readability, and maintainability of the global memory space, which is a `housekeeping` maintenance step that should happen whenever agents find it necessary, with approval from the operator, or when specifically prompted by the operator.

### Active VS Inactive Agents and Their Memory Usage

- Active agents are those currently engaged in tasks or processes within the system. They are expected to actively read from and write to the global memory space, ensuring that their actions and decisions are well-documented and accessible to other agents. Active agents should also monitor the global memory space for relevant updates from other agents, allowing them to adapt their strategies and actions accordingly.
- Inactive agents are those that are not currently engaged in any tasks or processes within the system. They may still hold data on the global memory space for future operations, so they should leave clear indications for anything that may still be relevant when they become active again, as well as clear indication for data that is no longer relevant so that any active agent knows it can be overwritten to free up memory resources for efficiency and readability, as `housekeeping` is the active agent's responsibility.

## Individual Memory Space

If the agent truly needs to store information that is not relevant to the other agents, it can use its own individual internal memory space. If there isn't one, the agent can create one at `.<agent_env_name>/memories/<memory>.md` relative to the repository root (eg.: `.claude/memories/MEMORY.md`, `.codex/memories/MEMORY.md`).

This space is not invisible to other agents, but its meant for one specific agent, which is the only one who should ever write to it. DO note, that any data there that IS or becomes relevant to the other agents MUST then be replicated to the global memory space to ensure that all agents have centralized, quick and easy access to teh relevant information for effective collaboration and decision-making.

## Plans and Tasks

```text
.agents/PLAN.md                 # Current Context, Overview, Collective Plans Summary
.agents/TASK.md                 # Current Context, Overview, Collective Tasks Summary
.agents/plans/<plan>.md         # Specific Plan Files
.agents/tasks/<task>.md         # Specific Task Files
```

In this multi-agent system, agents can create and manage plans and tasks to achieve specific goals. Plans are high-level strategies that outline the steps required to accomplish a goal, while tasks are individual actions or operations that contribute to the completion of a plan. Agents can collaborate on plans and tasks by sharing information, coordinating their actions, and updating the global memory space with their progress.

## Agent Handoff

Agents can initiate a handoff to another agent as needed. The handoff process involves transferring the relevant information, context, and responsibilities to the receiving agent, ensuring that the new agent can continue the work seamlessly. The handoff should be well-documented in the global memory space, including any pending tasks, decisions made, and any other relevant information that will help the receiving agent understand the current state of the work. This process ensures continuity and minimizes disruptions in the workflow.

## Rules of Engagement

This is a production repository. The code here runs in front of clients, and the
history is a record other people read. Two rules exist because they were broken
more than once.

### Prefer CLI over MCP

When a command-line interface and an MCP integration can both complete the same
operation, prefer the CLI. It is easier to reproduce, leaves a concise command
trail, and usually consumes less model context because it does not load broad
tool schemas or accessibility trees. For browser automation, prefer Playwright
CLI or repository tests when they provide the required browser and state.

Use MCP when the CLI is unavailable, when the task depends on a live session or
capability that the CLI cannot access, or when a higher-priority instruction
requires that integration. Do not install a new CLI only to avoid an already
available MCP without first considering the dependency and environment impact.

### Never commit without being asked

Writing a file and committing it are separate acts. Write, report what changed,
and stop. The operator commits, or asks for it explicitly.

A commit taken without asking removes the chance to simply fix the file before
it becomes history. "I needed a commit to deploy" is not a reason to skip
asking — say that the deploy needs a commit and wait.

The same applies to anything outward-facing: `git push`, force push, publishing,
and touching a remote. Ask first, every time.

Do not `git reset` or restage as a shortcut to committing. If the operator
arranged the index, that arrangement is a decision: files left outside the
staged area were left there on purpose.

### Never destroy `main`

`main` is production history. Rewriting it — reset, rebase, amend, reordering,
force push — is off limits, except for cleaning and fixing explicit mistakes, when very explicitly requested or authorized by the operator. If usual commits need to be reworked, that happens on another branch.

What may land directly on `main`, when touching git has been authorized, are **self-contained commits**: one that delivers a complete change and leaves
no loose end. This is just a matter of: "If this commit were the last one in the repository, would it let main in a consistent state? Would building main still pass? And deploying?". If the answer is no, it does not belongs there, do not commit it there.

Anything that needs more than one commit to serve a purpose larger than each
commit belongs on its own branch. Work there, and rework there — those branches are where a messy history is allowed to exist.

Inside a feature branch, commits may be progressive checkpoints instead of
complete deliverables. Prefer coherent groupings that make the work easier to
review, test, revert, and continue; an individual commit does not need to leave
the whole feature deployable. The branch as a whole must be cleaned and made
consistent before it is merged into `main`.

### Clean before merging

A branch is not merged by dragging everything in. Before it reaches `main`,
go back over it: fix what was left rough, drop what became dead, make the
comments and the naming consistent, squash what does not deserve to be a
separate commit.

Assume the branch carries the same habits that were corrected before, because
it usually does. What enters `main` has to be clean, consistent and
standardised — that is what keeps the history readable for whoever comes to it
without the conversation, and that is what makes it maintainable.

### Comments explain the code, never the bug

A comment says what the code does and why it exists. It never narrates the
defect that was just fixed, and never argues a case back to whoever asked a
question.

Wrong, and all real examples from this repository:

```text
# Naming what to stand down is the operator's call, not the repository's —
# the repository would be encoding one machine's previous tenant as if it
# were policy

# `{# #}` não serve aqui: a sintaxe curta é de uma linha só

# Incluí-lo faria o painel acusar "nome fora do padrão" ... e treinaria o
# operador a ignorar o aviso
```

Right:

```text
# DISABLE_SERVICES names systemd units to stand down, space separated.
```

The reasoning belongs in the reply and in the commit message. The file is read
by people who never saw the conversation.
