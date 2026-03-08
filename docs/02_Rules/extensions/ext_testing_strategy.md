# Extension: Testing Strategy

Purpose
- Mandate comprehensive testing strategies to prevent regressions in larger projects.
- To be used only when project scale is Production or explicitly required.

Rules
- All new business logic must have corresponding Unit Tests.
- Critical user journeys must be covered by End-to-End (E2E) tests.
- Maintain a minimum test coverage threshold (e.g., 80%).
- Tests must be run and pass locally before any pull request is submitted.
- Any bug fix must include a corresponding test case to prevent recurrence.
- Test files should be located alongside the code they test (e.g., `feature.ts` and `feature.test.ts`) or in a dedicated `tests/` directory as per project standards.
