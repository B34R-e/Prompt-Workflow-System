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

Post-execute gate (mandatory check, NOT mandatory update)
- After completing code changes, the agent MUST evaluate whether docs need updating:
  1. List files changed in this session
  2. Check against this mapping:
     - New sub-feature → 07_Features/{Area}.md row? _tracker.md count?
     - New API endpoint → 05_Detailed_Design/{Block}.md?
     - Any change → 09_Changes_History/changes_YYYY-MM-DD.md entry?
  3. If update needed → perform it (or flag to user)
  4. If no update needed → state "No doc update needed" with reason
- This is an evaluation step. Only update when the check says yes.