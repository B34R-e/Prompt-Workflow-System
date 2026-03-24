# 03_Architecture_Identify

Goal
- Produce 03_Architecture.md (Vietnamese) using:
  - 00_Project_Scope.md
  - 01_Problem_Definition.md
  - 02_Requirements.md
  - Architecture_Checklist.md

Agent behavior
- Architecture must guide construction: overview, building blocks, key decisions.
- Apply 80/20: describe the critical classes/components that drive most behavior.
- Keep it independent of specific language/machine where possible.
- Use Architecture_Checklist as sanity check; expand only where PARTIAL/FAIL.

Minimum content to generate (then adjust per scope)
1) Architectural overview: what exists and how it fits (include a simple diagram in text if needed)
2) Major building blocks: responsibilities + interfaces + communication rules (direct/indirect/forbidden)
3) Data design: major tables/files + ownership + access rules (information hiding)
4) Major classes (80/20): responsibilities + interactions + key state/persistence notes
5) Key business rules and their design impact
6) Error-handling strategy (coherent)
7) Resource management notes (only if relevant by scope/risk)
8) Buy-vs-build and reuse assumptions (only if relevant)

Checklist pass
- Run Architecture_Checklist with PASS/PARTIAL/FAIL/N/A.
- Address blockers first.
- Add “Architecture Health Summary” at the end (short).

Definition of Ready (DoR) for 03_Architecture.md
- Overall organization clear + justified
- Building blocks defined + mapped to requirements
- Critical classes described (80/20) + interactions
- Data design + DB organization decisions captured
- Coherent error-handling strategy
- Programmer comfort check: assumptions and risky areas explicit

Output rules
- Vietnamese output
- Typical length:
  - PoC: 1–2 pages
  - MVP: 2–4 pages
  - Production: 4–10 pages (more only if needed)