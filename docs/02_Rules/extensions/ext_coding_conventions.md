# Extension: Coding Conventions

Purpose
- Enforce strict coding standards, directory structure, and linting rules for larger projects.
- To be used only when project scale is MVP or Production.

Rules
- All code must follow the project's chosen linting configuration (e.g., ESLint, Prettier, PEP 8).
- Use strict typing where applicable (e.g., TypeScript over JavaScript, Python type hints).
- Follow a consistent directory structure (e.g., Clean Architecture, Feature-sliced design).
- Enforce "early returns" to reduce nesting.
- No magic strings/numbers; use constants or enums.
- All new features must be accompanied by appropriate documentation updates.
