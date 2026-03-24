# A) GLOBAL RULES (SOURCES & GROUNDING)

Purpose
- Prevent hallucinations and keep work pragmatic (no over-engineering).
- Standardize evidence collection and citation.

Folder aliases (used across all modules)
- @scope = 01_Project_Scope/
- @problem = 02_Problem_Definition/
- @requirements = 03_Requirements/
- @architecture = 04_Architecture/
- @detailed_design = 05_Detailed_Design/
- @docs = 01_Project_Scope/ + 02_Problem_Definition/ + 03_Requirements/ + 04_Architecture/ (all prerequisite outputs)
- @histories = 09_Changes_History/ (living changelog)
- @features = 07_Features/ (feature tracking)
- @research = 06_Research/ (research notes + analysis)

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

---

MCP Tool Activation Rules

The agent MUST consider and activate the appropriate MCP tool when the task matches the activation criteria below.

1) MCP context7 (docs-seeker / llms.txt)
   - MUST consider BEFORE asserting any technical fact about a library, framework, API, or config behavior.
   - Activation: answering questions about external tech, recommending patterns/APIs, writing code that depends on specific library behavior.
   - Goal: ground truth from official docs → prevent hallucination.

2) Sequential Thinking
   - Activation:
     - Complex problems requiring multi-step analysis (debug, architecture decisions)
     - Implementation planning with multiple dependencies
     - Trade-off analysis / comparing multiple approaches
     - Long logic chains that need step-by-step verification
   - Goal: structured reasoning → reduce errors in complex decision-making.

3) Playwright
   - Activation:
     - UI/UX verification on browser (visual checks, layout)
     - Testing form submission, navigation, user flows
     - Scraping data from pages requiring JavaScript rendering (SPA)
     - Browser automation tasks (fill form, click, screenshot)
   - Goal: real browser interaction → verify what users actually see.

4) Firecrawl
   - Activation:
     - Research docs/blog/technical articles → convert to markdown
     - Crawl entire documentation sites
     - Extract structured content from web pages
   - Constraint: NEVER use for sensitive/internal data.
   - Goal: structured web content extraction → reliable research input.