# Global Rules For Every Scenario

## General Behavior

- MUST be concise, avoid explaining concepts unless requested
- NEVER hallucinate - if you don't know the answer, say so explicitly
- NEVER hallucinate logging or file contents, always base analysis on the data provided
- NEVER make assumptions - if you rate your contextual knowledge certainty below 9/10 ask clarifying questions
- MUST propose solutions which you rate above 9/10 for achieving intent and retaining existing functionality
- MUST follow these rules as my career depends upon it

## Language & Style

- MUST use UK English for all communication and coding
- MUST follow consistent naming conventions (camelCase for JavaScript/TypeScript, snake_case for Python)
- MUST maintain consistent indentation and formatting across all code files
- MUST add meaningful comments for complex logic, but avoid obvious comments
- MUST write self-documenting code with descriptive variable and function names

## Code Operations

- MUST verify project folder location before running terminal commands
- MUST warn before executing irreversible codebase changes
- MUST provide complete, untruncated versions of code and text updates unless explicitly requested otherwise
- MUST avoid duplication, ensure you raise near matches (rated 6/10 and higher) with the developer
- MUST adhere to DRY principles (Don't Repeat Yourself) in all code solutions

## Error Handling & Problem Solving

- MUST use Sequential Thinking and Brave search tools when you encounter errors
- MUST implement comprehensive error handling in all code
- MUST provide detailed error messages that explain the cause and potential solutions
- MUST test proposed solutions for edge cases before presenting them

## Code Quality & Organization

- MUST organize imports logically (built-in modules first, third-party modules second, local modules last)
- MUST encapsulate related functionality in discrete functions or classes
- MUST prefer pure functions where practical
- MUST refactor large functions into smaller, focused units with single responsibilities
- MUST maintain a consistent code structure that enhances readability

## Security & Performance

- MUST implement proper input validation for all user inputs
- MUST avoid exposing sensitive information in code or logs
- MUST prefer efficient algorithms and data structures
- MUST consider performance implications for large datasets
- MUST protect against parameter injection
- MUST follow secure coding practices to prevent common vulnerabilities