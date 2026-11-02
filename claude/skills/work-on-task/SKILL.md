---
name: work-on-task
description: "Use when the user wants to start work on a task, given as a ticket ID (e.g. BL-012, #42, PROJ-123), a task file path, or a plain-text description. Runs a structured flow - read the task, explore the code, ask questions, get plan approval, implement, report."
argument-hint: "[ticket ID | task file path | description]"
---

# Work on Task

The task reference is whatever the user gave in their message or as skill arguments (ticket ID, file path, or description): $ARGUMENTS

If they gave none, ask which task to work on.

Follow these steps in order. Do not skip or combine steps without explicit user approval.

## Step 1 — Identify the task source

- A file path: read the file directly.
- A ticket number (e.g. `BL-012`, `#42`, `PROJ-123`): go to Step 2.
- Plain text: treat it as the task spec and skip to Step 3.

## Step 2 — Find the task management system (ticket numbers only)

1. Check `CLAUDE.md` (or `AGENTS.md`, if that is the project's instruction file) for a "Task Management" section.
2. If it is missing, look for clues in the repo: `backlog/` folders, `.github/`, Linear or Jira config files.
3. If still unclear, use the `AskUserQuestion` tool to ask which system is used and where tasks live.
4. Once confirmed, add a "Task Management" section to the project `CLAUDE.md` (or `AGENTS.md`) so future sessions skip this step.

Fetch the task with the matching tool: a file read for local backlogs, `gh issue view` for GitHub, or the configured MCP server for Jira or Linear. If the MCP server is not configured or requests fail (for example, authentication errors), stop and ask the user to set it up (`claude mcp add`, or `/mcp` to check or authenticate it) or to paste the task description.

## Step 3 — Read and understand the task

Extract:
- What needs to be built or changed
- Acceptance criteria, explicit or implied
- Constraints, dependencies, and technical notes

## Step 4 — Check the branch

The branch name should include the task number. If you are on a different branch, tell the user and ask whether to switch to or create the right one. Never work directly on `main` or `master`.

## Step 5 — Explore the codebase

Find everything relevant to the task. Run independent searches and reads in parallel, or delegate broad exploration to the `Explore` subagent (Agent tool). Understand:
- What already exists that the task touches or extends
- Which layers and modules are involved
- Related types, interfaces, and patterns already in use

Do not start planning until you have a solid picture of the existing code.

## Step 6 — Ask clarifying questions (if needed)

If ambiguities remain that would affect the implementation, ask them with the `AskUserQuestion` tool. Only ask what you cannot infer. Wait for the answers.

If everything is clear, say so explicitly and move on.

## Step 7 — Present an implementation plan

The plan should cover:
- What you will implement, broken into clear steps
- Which files will be created or modified, and why
- Architectural decisions and tradeoffs
- What you will NOT do (scope boundaries)

Present the plan and **wait for explicit approval**. Do not edit any files until the user approves. They may adjust, reject, or approve it.

## Step 8 — Implement

Execute the approved plan. Track progress with the todo list (`TodoWrite`, or the `TaskCreate`/`TaskUpdate` tools if those are available instead) and mark each step done as you finish it. If something unexpected requires a plan change, pause and flag it to the user before continuing. Run the project's linters and tests before reporting.

## Step 9 — Deliver a report

1. **What was done**: files created or modified and key decisions.
2. **What to test**: specific scenarios as a checklist.
3. **How to test**: concrete commands, UI flows, or API calls.

Do not change the task's status or close it in any tracker. The user handles that.
