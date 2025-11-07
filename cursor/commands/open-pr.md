# open-pr

Your task is to push your changes and open a pull request (PR).

1. Use available tools such as the GitHub CLI or the GitHub MCP tool. If neither is available, stop and ask the user to configure the MCP tool or CLI before proceeding.
2. Check your current branch. If you are on `main` or `master`, stop and ask the user to switch to a feature branch.
3. Run project linters and tests to ensure there are no linter issues or test failures. Look for the appropriate commands in the `Makefile` or `lets.yaml`.
4. Ensure all changes in the branch are committed. If there are uncommitted changes, review them and commit with concise messages. If the changes are substantial, split them into multiple self-contained commits.
5. Once all changes are committed, push the branch to GitHub.
6. Review all changes made in the current branch and draft a PR description. Share the draft with the user for review; do not open the PR until the user approves the description.
7. After receiving approval, open the PR using the approved description.
8. Provide the user with a link to the PR so they can review it further.