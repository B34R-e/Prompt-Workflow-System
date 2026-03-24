# 00_Project_Scope_Identify

Goal
- Interactively determine project scope/type and set documentation depth rules.
- Output is 00_Project_Scope.md (Vietnamese).

Agent behavior
- Ask only what is necessary to classify the project and create actionable scope.
- Prefer short questions; group them; stop when DoR is satisfied.

Questions (ask the user)
1) What is the product/system? (1–2 sentences)
2) Who are the primary users/stakeholders?
3) Project type (choose one):
   - Business system / Mission-critical / Life-critical (embedded life-critical)
4) Scale (choose one): PoC/Spike / MVP/Feature / Production
5) Constraints: deadline, compliance, data sensitivity, integrations, budget/timebox
6) Risk & cost of change:
   - What happens if we’re wrong? (low/med/high)
   - Is change late expensive? (low/med/high)
7) Success metrics:
   - What measurable outcome defines success?
8) Out of scope (top 3 “not doing” items)
9) Known unknowns (top 5 uncertainties)

Definition of Ready (DoR) for 00_Project_Scope.md
- Project summary (2–4 lines)
- Type + Scale
- Risk level + Cost-of-change level
- Constraints (top 5)
- Success metrics (1–3)
- Out of scope (top 3)
- Known unknowns (max 5)
- Required docs & depth:
  - Problem Definition: light/medium/deep
  - Requirements: light/medium/deep
  - Architecture: light/medium/deep
- Review cadence: when to re-check scope (e.g., per iteration / weekly / on trigger)

Output format for 00_Project_Scope.md (Vietnamese)
- Keep it short; bullets are preferred; 0.5–1.5 pages typical.