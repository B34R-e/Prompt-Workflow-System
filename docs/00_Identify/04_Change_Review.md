# 04_Change_Review

Goal
- Decide when to update: 00_Project_Scope.md, 01_Problem_Definition.md, 02_Requirements.md, 03_Architecture.md.
- Keep updates lightweight but disciplined.

When to run
- After each meaningful change cycle (end of day/iteration), or when a trigger occurs.

Triggers (2-of-5 rule)
Update docs if at least TWO are true:
1) Scope change: significant new/removed capability (≈ 10–20% functional impact).
2) New integration: new external system/interface/protocol introduced.
3) Nonfunctional change: performance/security/reliability targets changed.
4) Architectural decision change: new major building block, data ownership shift, or key design tradeoff changed.
5) Rework threshold: rework due to misunderstanding exceeds ~15–20% effort in a short window.

Immediate update (always)
- Problem definition or business case is invalidated.
- A blocker in Requirements_Checklist or Architecture_Checklist becomes FAIL.

What to update (mapping)
- Scope/business goal change → 00 + 01 + 02 (and maybe 03)
- Requirements change (functional) → 02 (and 03 if architecture affected)
- NFR change → 02 + 03
- New integration → 02 + 03
- Data model/ownership change → 03 (and 02 if requirements wording changes)
- UI strategy change → 03 (and 02 if user tasks/output change)

Output format (each review entry, short)
- Date
- What changed (1–3 lines)
- Triggers hit (list)
- Docs to update (00/01/02/03)
- Update now vs later (with reason)