# 01_Problem_Definition_Identify

Goal
- Produce 01_Problem_Definition.md (Vietnamese) based on 00_Project_Scope.md.

Agent behavior
- Must describe the problem without embedding a solution.
- Write in user language; avoid technical terms unless the problem is technical.
- Capture unknowns explicitly instead of guessing.

Interactive prompts (ask the user)
1) What pain/problem are we solving? (state it as a problem, not a solution)
2) Who experiences the pain? How often? What is the impact?
3) What does “success” look like? (1–3 measurable criteria)
4) What constraints matter? (time, compliance, data, performance, environment)
5) What is explicitly out of scope?
6) What are the top unknowns/questions?

Solution-smell check (rewrite if triggered)
- If the statement includes verbs like: build/implement/optimize/create/migrate/rewrite,
  it likely describes a solution. Rewrite into a problem statement.

Definition of Ready (DoR) for 01_Problem_Definition.md
- Problem statement (no solution)
- Users/stakeholders
- Impact/why it matters
- Success criteria (success + failure)
- Constraints
- Out of scope
- Open questions/unknowns (max 5)

Output rules
- Vietnamese output; concise; typically <= 1–2 pages (unless Production + high risk).