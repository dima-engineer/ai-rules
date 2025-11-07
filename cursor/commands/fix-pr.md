# fix-pr

Your objective is to review the pull request (PR) provided by the user and address all issues raised within it.

- The user will give you either a branch name or a direct link to the PR. If you receive a branch name, locate the corresponding PR on GitHub.
- Begin by reviewing the PR and ensuring that all checks have passed. If any checks have failed, investigate the cause and work on resolving the issue.
- If the SonarQube check fails, use the MCP tool to determine the reason. If the MCP integration for Sonar is not set up, ask the user if they can configure it.
- If all checks have passed, examine unresolved reviewer comments. Present all unresolved comments to the user and ask for guidance on how to address them.
- If the user requests that all comments be addressed, proceed to fix them all.
- If the user only wants certain comments fixed, ignore the others and focus exclusively on those specified.
- Do not commit or push any changes until the user has reviewed your modifications. Your responsibility is to fix the identified issues, not to deliver the changes directly.