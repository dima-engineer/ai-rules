---
name: Fix PR
description: Use when the user wants to fix a pull request, given as a branch name or PR link. Investigates failing checks (including SonarQube), collects unresolved reviewer comments, and fixes the ones the user chooses, without committing or pushing.
---

# Fix PR

Review a pull request (PR) and address the issues raised in it.

The user gives either a branch name or a PR link. For a branch name, find the matching PR with `gh pr list --head <branch>`. If they gave neither, use the PR for the current branch (`gh pr view`).

## Steps

1. **Checks**: run `gh pr checks` and confirm every check has passed. If any failed, find the cause (e.g. `gh run view <id> --log-failed`) and fix it.
2. **SonarQube**: if the SonarQube check fails, use the Sonar MCP server to find the reason. If it is not configured, ask the user whether they can set it up (`/mcps`).
3. **Review comments**: once checks pass, collect unresolved reviewer comments (`gh api` or the GitHub MCP server). Present them all to the user, with file and line, and ask how to handle them using the `question` tool.
4. **Scope**:
   - If the user wants all comments addressed, fix them all.
   - If the user wants only some, fix those and ignore the rest.
5. **Verify**: run the project's linters and tests after your changes.

## Constraints

- Do not commit or push. Leave the changes in the working tree for the user to review.
- Do not resolve or reply to PR comments unless the user asks.
- When done, summarize what you changed per comment or failing check.
