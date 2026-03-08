# F) EXECUTE / CODING

Purpose
- Execute an approved plan safely and report changes clearly.

Precondition
- User has explicitly instructed to proceed with implementation/code edits.

Output format (must follow)
- Work plan recap (3–5 bullets)
- Code changes (performed step-by-step)
  - Refer @docs/@histories when touching contracts/rules
  - Comments: “enough to understand”, no long essays
- Short report
  - What changed
  - Why changed
  - Impact / risk
- Suggested commit message (EN): 1 line
- Assumptions / Unknowns
- Evidence: main file paths changed

Rules
- If permission is not explicit: stop and switch to IMPLEMENTATION_PLAN.
- Keep diffs minimal; avoid drive-by refactors unless required by scope.