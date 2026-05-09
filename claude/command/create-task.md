You are creating a new backlog task from a high-level description. The user has provided: $ARGUMENTS

Follow these steps in order. Do not skip steps or combine them without explicit user approval.

---

## Step 1 — Understand the request

Read the user's description. Extract the core intent:
- What problem is being solved or what feature is being added?
- Which part of the system is involved (backend, frontend, infra, etc.)?

If no description was provided (i.e. $ARGUMENTS is empty), ask the user: "What task would you like to create?"

---

## Step 2 — Explore the codebase for context

Search the codebase for code, files, and patterns related to the task. Use grep, find, and file reads to understand:
- What already exists in this area
- Which layers / modules are relevant
- Any related types, interfaces, or domain concepts in use

This shapes the technical notes and acceptance criteria you'll write.

---

## Step 3 — Gather missing information (if needed)

If after reading the description and the code there are gaps — missing acceptance criteria, unclear scope, unknown constraints — prepare a numbered questionnaire for the user. Only ask what you genuinely cannot infer. Keep it tight.

Wait for answers before proceeding to Step 4.

If the description is already complete and unambiguous, skip this step and say so.

---

## Step 4 — Draft the task

Write a full task description using this structure:

```
## [TICKET-NNN] <Short imperative title>

**Status**: Backlog
**Priority**: <High / Medium / Low — infer from context or ask>
**Area**: <backend / frontend / infra / full-stack>

### Description

<2–4 sentences explaining what this task does and why it's needed.>

### Acceptance Criteria

- [ ] <concrete, testable criterion>
- [ ] <concrete, testable criterion>
- [ ] ...

### Technical Notes

<Optional. Key implementation hints, constraints, affected files/modules, or open questions for the implementer.>
```

Present the draft to the user and **wait for explicit approval**. The user may edit, reject, or approve.

---

## Step 5 — Identify the task management system

Check CLAUDE.md for a "Task Management" section that documents the system (e.g., Markdown files in `backlog/`, GitHub Issues, Linear, Jira).

If not documented:
1. Look for clues in the repo: `backlog/` folders, `.github/`, `linear.json`, etc.
2. Ask the user: "Where should I save this task? (e.g. a `backlog/` folder, GitHub Issues, Linear, etc.)"
3. Once confirmed, **persist the answer in the project-level CLAUDE.md** under a "Task Management" section so this step is skipped next time.

---

## Step 6 — Assign the ticket number

Inspect existing tickets to find the highest number used:
- For Markdown backlogs: list files in the backlog directory and parse the number from filenames (e.g. `BL-012-slug.md` → 012).
- For other systems: query the system for the last ticket number.

Increment by one for the new ticket (e.g. BL-012 → BL-013).

Update the ticket number in the draft.

---

## Step 7 — Save the task

Write the task to the appropriate location:
- **Markdown backlog**: create `<backlog-dir>/<PREFIX>-<NNN>-<kebab-title>.md` with the approved content.
- **GitHub Issues**: use `gh issue create` with title and body.
- **Other systems**: use the appropriate CLI or API.

Confirm to the user where the task was saved and show the final ticket number.
