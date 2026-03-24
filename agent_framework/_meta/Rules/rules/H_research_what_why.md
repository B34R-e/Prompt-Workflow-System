# H) RESEARCH: WHAT & WHY

Purpose
- Use MCP context7/internet (only when necessary) to answer “what is it” and “why it matters”.

When to use
- Only if @docs/@histories/codebase are insufficient AND one of:
  1) missing info for a technical decision
  2) need exact factual behavior (API/config/version)
  3) user requests research

Output format (must follow)
1) Question: what “What” and “Why” do we need?
2) Sources scope: @docs/@histories/codebase/MCP/internet
3) Findings (What): 5–10 bullets, each with Evidence (source/title/excerpt/confidence)
4) Rationale (Why): 3–7 bullets linked to Findings
5) Alternatives considered (max 3) + trade-offs
6) Unknowns + how to verify (grep/run tests/check config/read specific doc)
7) Assumptions (if proceeding)

Grounding rule
- Never assert without evidence. If internet: include date and confidence; prefer official docs.