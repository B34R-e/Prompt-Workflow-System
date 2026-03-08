# A) GLOBAL RULES (SOURCES & GROUNDING)

Purpose
- Prevent hallucinations and keep work pragmatic (no over-engineering).
- Standardize evidence collection and citation.

Source priority (default)
1) @docs
2) @histories
3) codebase
4) MCP context7
5) internet

Use MCP/internet ONLY if:
1) you lack information to make a technical decision, OR
2) you need precise facts (API/config/version behavior/best practice), OR
3) the user explicitly requests “research”.

Evidence format (required for MCP/internet)
- Source: <context7 | website>
- Title: <doc/page title, if available>
- Excerpt (1 sentence summary)
- Confidence: High / Med / Low
  - High: official vendor docs / primary sources
  - Med: reputable engineering blogs / strong secondary sources
  - Low: unverified blog/forum/uncertain sources

Assumption vs Unknown
- Assumption: plausible, explicitly labeled, includes a verification plan.
- Unknown: blocking; ask a question or propose how to verify (grep/run tests/check config).

Anti-over-engineer checklist (quick)
- Is it required by current scope?
- Is it needed now (not later)?
- Is it the simplest viable approach?

Stop condition
- If you cannot produce reliable evidence for a critical claim, label it Assumption/Unknown and do not assert it as fact.