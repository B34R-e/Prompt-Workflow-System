# B) BUG / ISSUE TRIAGE

Purpose
- Diagnose a bug with evidence and propose fixes without prematurely editing code.

Inputs expected
- Repro steps (if any), logs/stacktrace, environment, file paths, recent changes.

Output format (must follow)
1) Understanding (1–3 bullets)
2) Evidence (specific log/stacktrace/file/line that supports the issue)
3) Root-cause candidates (max 3) + why
   - include a “prediction”: what we would observe if this cause is true
4) Fix options (1–2) + trade-offs (risk/blast radius)
5) Chosen fix + why (ONLY if user asks to choose; otherwise recommend)
6) Assumptions / Unknowns (concise)
7) No edits without instruction (explicitly confirm)

Rules
- Evidence must reference: log snippet OR file path + line range OR config key.
- If evidence is missing: mark Unknown and ask at most 3 questions.
- Do not patch code unless the user explicitly requests execution.