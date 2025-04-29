# Agentic IDE Toolbox

A collection of structured prompts designed for agentic capabilities in modern IDEs. This repo was updated/migrated from the original architect framework as I felt there was too much overhead/admin in that approach, this is simpler, more efficient and a bit more self contained.

## TLDR;

1. Choose a prompt that matches your current agentic task:
   - `csr-*` prefix means designed for Cursor IDE
   - `roo-*` prefix means designed for Roo Code
   - No prefix means universal
2. In your tool of choice, reference and initiate with:

```markdown
Proceed with @prompt-file-name workflow
```

3. Some scripts have env variables you can set to save on calls/cost.
4. The AI assistant will guide you through a structured workflow.

## Overview

This repository provides step-by-step plans for common agentic tasks that can be used with AI-powered assistants like GitHub Copilot, Cursor, Roo, and other LLM-integrated coding tools.

These prompts are designed to be adaptable across different agentic coding tools and workflows, giving developers flexibility in how they implement them. If you dont find a prompt specific to your agentic tool of choice, take the base and update it to reference tools available in your agentic tool of choice, or mcp servers you have installed that offer comparable features i.e for web search in cursor you can use `web_search` or you can reference `brave_web_search` if you have the brave mcp server installed etc.

These prompts are designed to be flexible templates. Feel free to modify them to better suit your specific development environment and workflow requirements.

## Extended Workflow Prompts

The following new prompts have been added to enhance the agentic IDE experience:

- `orchestrator.md` (located in `planning-tasks/`): Provides an orchestration workflow for solution design, including dependency verification, task prioritisation, and building comprehensive project context.
- `tdd-task-coder.md` (located in `coding-tasks/`): Tailored for test-driven development, guiding developers to create tests first which drive their implementation.

Note: `csr-solution-designer.md`, `orchestrator.md`, and `tdd-task-coder.md` work seamlessly together and will be updated to trigger each other automatically when Cursor supports mode switching. Additionally, by limiting the context provided for each task to a need-to-know basis, we lower operational costs; hence, the introduction of the `active-task.md` concept.

## Repository Structure

```
agentic-ide-toolbox/
├── planning-tasks/       # Planning and architecture prompt templates
│   ├── csr-solution-designer.md
│   └── roo-solution-designer.md
├── coding-tasks/         # Coding and implementation prompt templates
│   ├── tdd-coder.md
│   ├── tdd-unit-test-debugger.md
```

## Available Prompts

### Planning Tasks

- **Solution Designer** (`planning-tasks/csr-solution-designer.md` or the roo variant): Guides an AI assistant through creating comprehensive solution documentation including product requirements, technical approach, and task breakdown.

- **Orchestration** (`planning-tasks/orchestrator.md`): Provides an orchestration workflow for task implementation, including dependency verification, task prioritisation, and building comprehensive project context - best paired with the solution-designer.md and tdd-task-coder.md.

- **prd-creator** (`planning-tasks/orchestrator.md`): Guides an AI assistant through creation of product requirements document, is opinionated about initial prioritsation based on the project delivery type (prototype vs full product)

### Coding Tasks

- **Test-Driven Development & Orchestration** (`coding-tasks/tdd-coder.md`): Structured workflow for implementing features using test-driven development methodology, orchestrator and feature implementation - best paired with the solution-designer.md task output.
- **Test-Driven Debugging** (`coding-tasks/tdd-unit-test-debugger.md`): Systematic approach for debugging code issues using tests to verify fixes.
- **Test-Driven Development** (`coding-tasks/tdd-task-coder.md`): Structured workflow for implementat feature using test-driven development methodology - simplified version fo tdd-coder that only focuses on feature implementation - best paired with the orchestrator.md.

### Documentation Tasks

- **Knowledge base creator** (`documentation-tasks/kb-generator.md`): Facilitates the generation of a technical knowledge base, offering detailed documentation with best practices, examples, and troubleshooting guidance.

### Coming Soon

- UX Design prompts
- And more...

## Contributing

Contributions are welcome! If you have ideas for new prompt templates or improvements to existing ones, please open an issue or submit a pull request.

## License

This project is licensed under the terms of the included LICENSE file.
