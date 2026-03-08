# 02_Requirements_Identify

Goal
- Produce 02_Requirements.md (Vietnamese) using:
  - 00_Project_Scope.md
  - 01_Problem_Definition.md
  - Requirements_Checklist.md

Agent behavior
- Build requirements to the depth specified in 00_Project_Scope.md.
- Use the checklist as a sanity check; expand only where checklist items are PARTIAL/FAIL.
- Do not over-specify design. Keep requirements testable.

Process
1) Draft requirements (initial pass) with minimal structure:
   - Functional: user tasks + inputs/outputs + data per task
   - Nonfunctional: response time/timing/security/reliability/resources/maintainability
   - Success & failure definition
   - Assumptions/unknowns
2) Run Requirements_Checklist:
   - Mark PASS/PARTIAL/FAIL/N/A
   - Fix blockers first (Critical items)
3) Produce a short “Requirements Health Summary” at the end:
   - PASS/PARTIAL/FAIL counts
   - Top 3 risks + actions
   - Unknowns (max 5)

Definition of Ready (DoR) for 02_Requirements.md
- Functional scope: tasks + inputs/outputs + data per task
- Nonfunctional essentials: at least performance/security/reliability expectations (or explicitly N/A)
- Clear success/failure definition
- Requirements are testable (acceptance criteria for top scenarios)
- No major conflicts
- Unknowns & expected changes documented

Output rules
- Vietnamese output
- Typical length:
  - PoC: 0.5–1.5 pages
  - MVP: 1–3 pages
  - Production: 3–7 pages (more only if compliance demands it)