---
name: create-task
description: Use when the user wants to create a new backlog task, ticket, or issue from a high-level description. Explores the code, asks missing questions, drafts the task for approval, assigns the next ticket number, and saves it to the project's task system.
---

# Create Task

The task description is whatever the user gave in their message. If they gave none, ask: "What task would you like to create?"

Follow these steps in order. Do not skip or combine steps without explicit user approval.

## Step 1 — Understand the request

Extract the core intent:
- What problem is being solved or what feature is being added?
- Which part of the system is involved (backend, frontend, infra, etc.)?

## Step 2 — Explore the codebase for context

Search for code, files, and patterns related to the task. Run independent searches in parallel. Understand:
- What already exists in this area
- Which layers and modules are relevant
- Related types, interfaces, and domain concepts

This shapes the technical notes and acceptance criteria.

## Step 3 — Gather missing information (if needed)

If there are gaps (missing acceptance criteria, unclear scope, unknown constraints), ask with the ask questions tool. Only ask what you cannot infer. Wait for the answers.

If the description is complete and unambiguous, skip this step and say so.

## Step 4 — Draft the task

Use this structure:

```
## [TICKET-NNN] <Short imperative title>

**Status**: Backlog
**Priority**: <High / Medium / Low, inferred from context or asked>
**Area**: <backend / frontend / infra / full-stack>

### Description

<2–4 sentences explaining what this task does and why it's needed.>

### Acceptance Criteria

- [ ] <concrete, testable criterion>
- [ ] <concrete, testable criterion>

### Technical Notes

<Optional. Implementation hints, constraints, affected files or modules, open questions.>
```

Present the draft and **wait for explicit approval**. The user may edit, reject, or approve it.

## Step 5 — Identify the task management system

1. Check `AGENTS.md` and `.cursor/rules/` for a "Task Management" section (e.g. Markdown files in `backlog/`, GitHub Issues, Linear, Jira).
2. If it is missing, look for clues in the repo: `backlog/` folders, `.github/`, `linear.json`, etc.
3. If still unclear, ask with the ask questions tool where the task should be saved.
4. Once confirmed, add a "Task Management" section to the project `AGENTS.md` so this step is skipped next time.

## Step 6 — Assign the ticket number

Find the highest number in use:
- **Markdown backlog**: list the backlog directory and parse numbers from filenames (`BL-012-slug.md` → 012).
- **Other systems**: query the system for the last ticket number.

Increment by one (BL-012 → BL-013) and update the draft.

## Step 7 — Save the task

- **Markdown backlog**: create `<backlog-dir>/<PREFIX>-<NNN>-<kebab-title>.md` with the approved content.
- **GitHub Issues**: run `gh issue create` with the title and body.
- **Other systems**: use the appropriate CLI or MCP tool.

Confirm where the task was saved and show the final ticket number.
