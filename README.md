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
4. The AI assistant will guide you through a structured workflow.

## Overview

This repository provides step-by-step plans for common agentic tasks that can be used with AI-powered assistants like GitHub Copilot, Cursor, Roo, and other LLM-integrated coding tools.

These prompts are designed to be adaptable across different agentic coding tools and workflows, giving developers flexibility in how they implement them. If you dont find a prompt specific to your agentic tool of choice, take the base and update it to reference tools available in your agentic tool of choice, or mcp servers you have installed that offer comparable features i.e for web search in cursor you can use `web_search` or you can reference `brave_web_search` if you have the brave mcp server installed etc.

These prompts are designed to be flexible templates. Feel free to modify them to better suit your specific development environment and workflow requirements.

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

### Coding Tasks

- **Test-Driven Development** (`coding-tasks/tdd-coder.md`): Structured workflow for implementing features using test-driven development methodology - best paired with the solution-designer.md task output.
- **Test-Driven Debugging** (`coding-tasks/tdd-unit-test-debugger.md`): Systematic approach for debugging code issues using tests to verify fixes.

### Coming Soon

- UX Design prompts
- Documentation generators
- And more...

## Contributing

Contributions are welcome! If you have ideas for new prompt templates or improvements to existing ones, please open an issue or submit a pull request.

## License

This project is licensed under the terms of the included LICENSE file.
