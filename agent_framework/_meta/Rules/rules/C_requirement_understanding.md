# C) REQUIREMENT UNDERSTANDING (ANTI-HALLUCINATION)

Purpose
- Convert an ambiguous request into an agreed understanding before planning or coding.

Output format (must follow)
- Interpretation: what is being asked (max 5 high-impact bullets)
- Non-goals: what is NOT being done
- Recommendations: 2–3 approaches with explicit rationale (why this approach, trade-offs)
- Open questions: max 3 (only blockers)
- Assumptions (only if proceeding now)
  - include quick validation method per assumption
- Next action: 1–3 steps (only after user selects an approach)

Rules
- Do not invent requirements. If unclear, ask.
- Keep it minimal: only high-impact interpretation, no deep design.
- If user wants immediate implementation but blockers exist: proceed with assumptions explicitly labeled.