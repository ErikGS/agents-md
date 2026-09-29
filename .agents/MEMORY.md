# Collective memory

Index of the memory shared among this repository's agents. This file is a
summary and map: **content belongs in the memory files**, never here.

## Before anything else

`.agents/AGENTS.md` is mandatory reading and takes precedence over any habit. It
contains this repository's working rules, including two that have already been
broken more than once:

- **do not commit without a request** — writing a file and committing are
  separate acts, and the same applies to pushing and anything that leaves here;
- **do not destroy `main`** — history is rewritten on another branch, and
  anything that enters `main` arrives clean and reviewed.

This is a production repository. What is here runs in front of customers.

## Where everything lives

```text
.agents/AGENTS.md              working instructions — mandatory
.agents/MEMORY.md              this index
.agents/memories/<name>.md     durable context, one subject per file
.agents/PLAN.md                index of open plans
.agents/plans/<name>.md        plan in progress; removed when executed
.agents/TASK.md                index of open tasks
.agents/tasks/<name>.md        task in progress; removed when completed
```

The distinction that keeps this usable: **memory describes what is**, while
plans and tasks describe **what to do**. Executed plans and completed tasks are
discarded; whatever deserved to survive becomes memory.

Product and operational documentation (intended for the team or end user) does
not belong here — it belongs in `docs/` (e.g. `docs/<deployment>.md`,
`docs/wiki/<wiki>.md`, etc.) and should be written professionally.

## Memories

- [workflow](memories/workflow.md) — about the work cycle with the operator
- [plan-template](memories/plan-template.md) — plan template, with steps A, B, and C, to serve as a basis for real plans.

## Current state

Plan [example-plan](plans/example-plan.md) archived.
