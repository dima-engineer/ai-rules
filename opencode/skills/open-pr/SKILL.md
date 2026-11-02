---
name: Open PR
description: Use when the user wants to push their changes and open a pull request. Runs linters and tests, commits, pushes, drafts the PR description for approval, then opens the PR with the GitHub CLI or MCP.
---

# Open PR

Push the current changes and open a pull request (PR). Use any extra context the user gave in their message (base branch, ticket, reviewers).

## Steps

1. **Tooling**: use the GitHub CLI (`gh`) or a configured GitHub MCP server. If neither is available, stop and ask the user to set one up (`/mcps` for MCP).
2. **Branch**: run `git branch --show-current`. If it is `main` or `master`, stop and ask the user to switch to a feature branch.
3. **State**: run `git status --short` and `git log --oneline -10` in parallel to see what is uncommitted and what commit style the repo uses.
4. **Checks**: run the project's linters and tests. Look for commands in `AGENTS.md`, the `Makefile`, `lets.yaml`, or `package.json`. Fix failures before continuing.
5. **Commit**: if there are uncommitted changes, review them with `git diff` and commit with concise messages that follow the repo's commit style. Keep every commit small, atomic, and independent: one logical change per commit that stands on its own. Never commit secrets or unrelated files.
6. **Push**: push the branch to GitHub, setting the upstream if needed. Never force-push.
7. **Draft**: review all changes on the branch against its base (`git diff <base>...HEAD`, `git log <base>..HEAD`) and draft a PR title and description. If a `PR_TEMPLATE.md` file exists in this skill's directory (next to this `SKILL.md`), follow it: it either is the template or says where to get one. Show the draft to the user. **Do not open the PR until the user approves it.**
8. **Open**: after approval, create the PR with `gh pr create` using the approved text.
9. **Report**: give the user the PR link.
