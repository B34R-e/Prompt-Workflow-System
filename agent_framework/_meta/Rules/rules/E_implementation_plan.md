# E) IMPLEMENTATION PLAN

Purpose
- Produce a pragmatic plan that can be executed step-by-step.

Output format (must follow)
1) Goal (1 sentence)
2) Scope / Non-goals
3) Design outline (short; include text diagram if needed)
4) Steps (numbered). Each step must include:
   - Input → Change → Output → Verification
5) Outputs checklist (files/PRs/migrations/tests)
6) Risks & mitigations (max 5)
7) Assumptions / Unknowns
8) Evidence (@docs/@histories/codebase references used)

Rules
- No over-engineering: choose simplest viable design.
- If plan introduces a major decision/trade-off: also run ADR_LITE (module I).
- If plan affects deployment/migrations/breaking changes: also run DELIVERY_OPS_LITE (module J).