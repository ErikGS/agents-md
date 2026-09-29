# Example plan

This plan defines and validates the creation of a reusable template for implementation plans.

Objective: generate a standardized Markdown file to record the objective, status, approval, progress, tests, commits, and execution steps.

## Status

### Archived

`Archived` by operator `ExampleOperator` on `2026-09-29 15:29:01 UTC-03:00`. Executor: `GPT-5 via GitHub Copilot in VS Code`.

### Requirements:

- Define the standard template structure.
- Include possible plan statuses.
- Record approval, executor, branch, and testing strategy.
- Represent progress with valid Markdown checkboxes.
- Include space for an overview, steps, and future topics.

### Progress

- [ ] A: Define the template structure and fields
- [ ] B: Write the template Markdown file
- [ ] C: Review the consistency and validity of the Markdown syntax
- [ ] Operator test and commit.

### Observations / Notes / Comments / etc.

The operator tests `at the end of each step`,
in the order `A → C`; commit `only after their approval`, on the `feature/plano-template` branch.

## Overview

The template should serve as a starting point for implementation plans. It must clearly distinguish the plan status, pending conditions, progress for each step, validation strategy, and items that are out of scope.

The expected result is a readable, reusable Markdown file compatible with common Markdown renderers, without ambiguous syntax for checkboxes or commit links.

Success criteria:

- The file contains all fields necessary to track a plan.
- Checkboxes use only `[ ]` and `[x]`.
- Commit links use valid Markdown.
- The steps are independent and verifiable.
- The template can be copied to start a new plan without requiring structural changes.

## A. Define the template structure and fields

- Confirm the template title and description.
- Define the objective field.
- Define the possible statuses.
- Define the approval, executor, branch, and commit fields.
- Define the requirements, progress, observations, and overview sections.

## B. Write the template Markdown file

- Create the title `# Plan template`.
- Add placeholders for plan-specific information.
- Add steps A, B, and C as examples.
- Add the operator test and commit item.
- Add the out-of-scope topics section.

## C. Review the consistency and validity of the Markdown syntax

- Verify that all checkboxes are valid.
- Verify that commit links are correctly formatted.
- Verify that the placeholders are understandable.
- Confirm that the status flow contains no contradictions.
- Perform a simulation by filling the template with a fictional plan.

## Discuss later (outside this plan)

- Automate the creation of new plans.
- Add automatic format validation.
- Define conventions for branch and commit names.
