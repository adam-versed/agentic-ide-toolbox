# Agentic IDE Toolbox

A collection of structured prompts designed for agentic capabilities in modern IDEs.

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
4. The AI assistant will guide you through a structure workflow.

## Overview

This repository provides step-by-step plans for common agentic tasks that can be used with AI-powered assistants like GitHub Copilot, Cursor, Roo, and other LLM-integrated coding tools.

These prompts are designed to be adaptable across different agentic coding tools and workflows, giving developers flexibility in how they implement them.

These prompts are designed to be flexible templates. Feel free to modify them to better suit your specific development environment and workflow requirements.

## Repository Structure

```
agentic-ide-toolbox/
├── planning-tasks/       # Planning and architecture prompt templates
│   ├── csr-solution-designer.md
│   ├── csr-task-planner.md
│   └── roo-solution-designer.md
├── coding-tasks/         # Coding and implementation prompt templates
│   ├── tdd-coder.md
│   ├── tdd-debugger.md
│   └── unit-test-failure-analysis.md
└── global-rules/         # Project-wide rules and guidelines
    └── system-wide-rules.md
```

## Available Prompts

### Planning Tasks

- **Solution Designer** (`planning-tasks/csr-solution-designer.md`): Guides an AI assistant through creating comprehensive solution documentation including product requirements, technical approach, and task breakdown.

### Coding Tasks

- **Test-Driven Development** (`coding-tasks/tdd-coder.md`): Structured workflow for implementing features using test-driven development methodology.
- **Test-Driven Debugging** (`coding-tasks/tdd-debugger.md`): Systematic approach for debugging code issues using tests to verify fixes.

### Coming Soon

- UX Design prompts
- Documentation generators
- And more...

## Contributing

Contributions are welcome! If you have ideas for new prompt templates or improvements to existing ones, please open an issue or submit a pull request.

## License

This project is licensed under the terms of the included LICENSE file.
