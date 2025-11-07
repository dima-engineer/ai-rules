# work-on-task

You will be given a Jira ticket ID.

1. Fetch the task using the Jira MCP tool. If MCP is not installed or if Jira requests fail (e.g., due to authentication errors), pause and ask the user to set up the MCP tool before proceeding or manually providing task description
2. Ensure you are on the correct branch. The branch name should include the provided task number.
3. Investigate any parts of the codebase that may be relevant to the task.
4. Compile a list of questions that will help clarify the requirements and enable you to create a detailed work plan.
5. After the user has answered all your questions, present your proposed work plan for review. Do not begin implementation at this stage.
6. Begin work on the task only after the user has approved the plan.