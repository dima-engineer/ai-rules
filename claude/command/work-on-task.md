You are starting a structured task implementation flow. The user has provided a task reference: $ARGUMENTS

Follow these steps in order. Do not skip steps or combine them without explicit user approval.

---

## Step 1 — Identify the task source

Determine what was provided:
- A file path → read that file directly
- A task/ticket number (e.g. BL-012, #42) → proceed to Step 2
- A plain text description → treat it as the task spec; skip to Step 3

## Step 2 — Identify and learn the task management system (only if a task number was given)

Check CLAUDE.md for documented task management info. If not documented:
1. Look for clues in the repo: `backlog/` folders, `.github/`, Linear/Jira config files, etc.
2. Ask the user: "What task management system are you using and where are the task files?"
3. Once confirmed, **persist the answer in the project-level CLAUDE.md** under a "Task Management" section so this step is skipped in future sessions.

## Step 3 — Read and understand the task

Read the full task spec. Extract:
- What needs to be built or changed
- Acceptance criteria (explicit or implied)
- Any constraints, dependencies, or technical notes in the task

## Step 4 — Explore the codebase

Find all files and code relevant to the task. Use search, grep, and file reads to understand:
- What already exists that the task touches or extends
- Which layers / modules are involved
- Any related types, interfaces, or patterns already in use

Be thorough. Do not start planning until you have a solid picture of the existing code.

## Step 5 — Prepare a clarifying questionnaire (if needed)

If after reading the task and the code there are still ambiguities that would affect the implementation, write a numbered list of questions for the user. Keep it tight — only ask what you genuinely cannot infer. Wait for answers before proceeding.

If everything is clear, skip this step and say so explicitly.

## Step 6 — Present an implementation plan

Write a detailed plan covering:
- What you will implement (broken into clear steps)
- Which files will be created or modified, and why
- Any architectural decisions or tradeoffs
- What you will NOT do (scope boundaries)

Present the plan to the user and **wait for explicit approval** before writing any code. The user may adjust, reject, or approve the plan. Do not start implementation until they say to proceed.

## Step 7 — Implement

Execute the approved plan. Mark each step done as you complete it. If you discover something unexpected mid-implementation that requires a plan change, pause and flag it to the user before continuing.

## Step 8 — Deliver a report

Once implementation is complete, provide:
1. **What was done** — a concise summary of changes made (files created/modified, key decisions)
2. **What to test** — specific scenarios the user should verify, written as a checklist
3. **How to test** — concrete steps (commands to run, UI flows to walk through, API calls to make)

## Step 9 — Mark task as done

When the user confirms the task is complete, mark it as done in whatever system the task came from:
- **Local file-based backlog**: set `**Status**: Done`, check all acceptance criteria checkboxes (`- [x]`), and move the file to the `done/` subfolder if one exists alongside it
- **GitHub Issues / PRs**: close the issue or mark the PR as ready
- **Linear / Jira / other**: update the status to Done/Closed via the appropriate API or tool
- **Plain text description**: nothing to update — just confirm completion to the user
