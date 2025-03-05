# AI-Assisted IDE Coding Workflows

This directory contains two workflow definition files designed for AI-assisted development in modern IDEs in combination with the Architect framework generated supporting documentation:

## Available Workflows

### 1. Full Coding Workflow (usage with Architect mini)

A comprehensive workflow suitable for complex, enterprise-level projects that require:

- Full documentation validation
- Architectural compliance checks
- Data schema verification
- Detailed user flow validation
- Rigorous task tracking

### 2. Mini Coding Workflow (usage with Architect full)

A streamlined version ideal for:

- Smaller projects
- Rapid prototyping
- Individual components
- Quick iterations

## Key Differences

| Feature                | Full Workflow | Mini Workflow |
| ---------------------- | ------------- | ------------- |
| Required Doc Files     | 6 files       | 2 files       |
| Architecture Diagrams  | Required      | Not Required  |
| User Flow Validation   | Required      | Not Required  |
| Data Schema Validation | Required      | Not Required  |

## Common Features

Both workflows share core functionalities:

- Task selection and prioritisation
- Test-Driven Development (TDD) approach
- Automated testing integration
- Task status tracking
- Event-driven development process

## Usage

1. Choose your workflow based on project scope and usage of Architect framework (full|mini):

   - Use [full-coding-workflow.md](full-coding-workflow.md) for enterprise/complex projects
   - Use [mini-coding-workflow.md](mini-coding-workflow.md) for smaller/rapid development

2. Decide how best to implement the system prompt

   - in cursor its effective as .cursorrules file in root
   - alternatively store a .md version in your .docs folder (sometimes more flexible, less token usage)

3. Configure the variables:

   ```
   DOCS_PATH = path-to-your-build-docs
   BUILD_COMMAND = your-package-manager-build-command
   TEST_COMMAND = your-global-test-command
   ```

4. Initiate:

   ```
   Initiate workflow as per (@.cursorrules|@full-coding-workflow.md etc.)
   ```

5. Follow the three-step workflow:

   - Review tasks
   - Implement task
   - Update task status

## Test approach and use of build compilation

- the use of both build command test command enable:
  - handling of early stage builds before test framework in place
  - ensures there isnt a backlog of early failures to address
  - allows for a less TDD approach when building a prototype

## Event Triggers

Both workflows implement three main triggers:

- `ON_TASK_REVIEW`
- `ON_TASK_ACTIVE`
- `UPDATE_TASK_STATUS`

## Best Practices

1. **Gotchas**

   - Watch for the 🤖 emoji to confirm prompt context retention
   - Favour starting next task in a new chat window to keep context size down (same initialise step)
   - Watchout for duplication of code (its less with system, but still happens)
   - Watchout for unnecessary bespoke implementation when ready made packages available

2. **Documentation Location**

   - Keep all files in `.doc` folder
   - Ensures clean project initialisation
   - Maintains separation from source code

3. **IDE Integration**

   - Use IDE-specific system wide rules to reinforce global behaviour (for cursor, see User Rules)
   - IDE agents are general in nature:
   - Give them specialised docs focusing on particular tech (see [mermaid_best_practices.md](mermaid_best_practices.md) or [Unit test analysis doc](unit-test-failures-analysis.md))
   - If cursor make use of .mdc tied to specific file types (targetted knowledge)

4. **Unit tests**

- You can get stuck in loops when trying to solve many or complex unit test failures via agentic control
- Claude 3.7 sonnet with deep thinking is a lot better of breaking out of these loops than claude 3.5 sonnet
- If repeated failures to fix, try asking your assistant to add more logging around the issue (this is largely what cladue 3.7 does differently)
- If your IDE Assistant is set to automatically fix linting issues, I would turn this off whilst addressing unit test failures and fix the linting after, it can make the situation too complicated.
- If have many failures, try and alter the test run commmand to focus on specific test(s) so it can brute force rather than jumping back and forth
- If you can see failures around a specific 3rd party tool - try finding a readme or knowledge base and adding it to your project as a local doc for context and let the LLM know on the next pass e.g. I have a jest best practices doc and a file focused on a method for analysing unit tests failures
- This short prompt is often helpful for more focused fixing of unit tests (requires MCP, but can be adapted to your IDE/LLM):

```markdown
1. Run yarn test and note the failures
2. Use the analysis approach outlined in @unit-test-failure-analysis.md and review the test failures noted in step 1.
3. Review the project @technical-approach.md
4. Use Sequential Thinking to form a search query on the failures for Brave search. Use Brave search to Identify up to 3 solutions that score at least 9/10 for probability to fix the issue(s).
```

- [Unit test analysis doc](unit-test-failure-analysis.md) is used in the above prompt

## Contributing

Feel free to submit issues and enhancement requests to improve the system.

These ensure consistent development practices regardless of workflow choice.
