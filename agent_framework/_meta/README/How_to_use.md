# How_to_use.md

This document explains how to use the agent docs in a short, practical way.

---

## 0) What is what

### OUTPUT files (Vietnamese) — SDLC Phases
These are the deliverables you maintain per project:
- 01_Project_Scope/Project_Scope.md
- 02_Problem_Definition/Problem_Definition.md
- 03_Requirements/Requirements.md
- 04_Architecture/Architecture.md (HLD)
- 05_Detailed_Design/_overview.md + per-block files (construction phase)

### CONTROL files (English) — Meta/Tooling
These guide the agent on how to produce / update the outputs:
- _meta/Rules/Agent_Rules.md (entry point + routing + output routing map)
- _meta/Identify/00_Project_Scope_Identify.md
- _meta/Identify/01_Problem_Definition_Identify.md
- _meta/Identify/02_Requirements_Identify.md
- _meta/Identify/03_Architecture_Identify.md
- _meta/Identify/04_Change_Review.md
- _meta/Checklist/Requirements_Checklist.md
- _meta/Checklist/Architecture_Checklist.md
- _meta/Checklist/Upstream_Prerequisites_Checklist.md
- _meta/Checklist/Major_Construction_Practices_Checklist.md
- _meta/Rules/rules/A_global.md … _meta/Rules/rules/J_delivery_ops_lite.md
- _meta/Rules/Breaking_Changes_Update_Rules.md (how to update paths when structure changes)
- _meta/Rules/Claude_Code_Bridge_Rules.md (integration pattern when using Claude Code + ClaudeKit)
- _meta/README/Migration_Guide.md (sync project to latest B34R-e structure)
- **_meta/Rules/extensions/**: Conditional rules dynamically loaded for Production/MVP scale (e.g. `ext_coding_conventions.md`, `ext_testing_strategy.md`, `ext_security_audit.md`).

### HISTORY files
Living changelog — only active/applied changes, reverted ones are removed:
- 09_Changes_History/changes_YYYY-MM-DD.md

### FEATURE TRACKING files (Vietnamese)
Per-area feature tracking — monitor sub-features and status:
- 07_Features/_tracker.md (overview table)
- 07_Features/<Area>.md (one file per feature area)

### RESEARCH & ANALYSIS files
Scratchpads — the agent writes here during deep dives before implementation:
- 06_Research/ (research notes from H_research_what_why module)
- 06_Research/analysis/ (analysis documents, implementation plans)

### REFERENCE files
Shared context — read-only for the agent workflow, updated manually or by specific modules:
- 08_Business_Flow/ (business flow documentation)
- 10_Common/ (API, Database, UI/UX, Security, Testing references)
- 11_Environment/ (setup, onboarding, deployment guides, and project Runbook)

---

## 0.5) First-time setup (one-time only)

### Path A — Standalone (no Claude Code / no ClaudeKit)

1. Copy the `agent_framework/` folder from B34R-e template into your project.
2. Rename to `agent-framework/` (recommended) or keep as `agent_framework/`.
3. Proceed to Step 1.

No additional setup needed.

### Path B — With Claude Code + ClaudeKit

1. Copy the `agent_framework/` folder from B34R-e template into your project as `agent-framework/`.
2. Give the agent the following prompt to create the bridge:

**Template prompt (bridge setup):**

> Read `agent-framework/_meta/Rules/Claude_Code_Bridge_Rules.md`.
> Execute all steps in Sections 2, 6, and 7:
> - Rewrite `CLAUDE.md` at project root (Section 2A).
> - Create `.claude/rules/primary-workflow.md` (Section 2C).
> - Create `.claude/rules/documentation-management.md` (Section 2D).
> - Update `.claude/rules/development-rules.md` — keep YAGNI/KISS/DRY inline, add redirect (Section 2B).
> - If `AGENTS.md` exists, update its workflows section (Section 2E).
> - Create `.mcp.json` at project root from template (Section 2F). If already exists, merge new servers.
> - Delete deprecated `docs/` folder at project root if it exists (Section 6).
> - Run verification checklist (Section 7) and show results.
> - Remind user to fill API keys in `.mcp.json` (CONTEXT7_API_KEY, FIRECRAWL_API_KEY).

3. (Optional, recommended) Set up the Confirmation Gate hook for hard enforcement:

> Read `agent-framework/_meta/Rules/Claude_Code_Bridge_Rules.md` Section 5.
> Execute:
> - Create `.claude/hooks/confirmation-gate.sh` from template (Section 5F).
> - Merge hook config into `.claude/settings.json` (Section 5G).
> - Add `.claude/.confirmation_state` to `.gitignore`.
> - Run verification: test that Edit is blocked without state file, allowed with state file.

4. Verify CK hooks still work (start new session, check rules injection).
5. Proceed to Step 1.

### Re-running setup
This setup is **idempotent** — re-run the same prompt anytime to sync with latest framework changes.
The agent will check existing files and update/create only what's needed.

### Notes
- Path A and Path B produce the same structure. Path B adds a thin bridge layer to `.claude/`.
- The bridge does NOT modify B34R-e content or CK content — it is project-level glue only.
- Full bridge spec: `_meta/Rules/Claude_Code_Bridge_Rules.md`.

---

## 1) Start a new project (initialization)

### Step 1 — Create scope
Ask the agent to:
- Read: Agent_Rules.md + _meta/Identify/00_Project_Scope_Identify.md
- Interact with you (short Q&A)
- Output (Vietnamese): 01_Project_Scope/Project_Scope.md

### Step 2 — Create problem definition
Ask the agent to:
- Read: Agent_Rules.md + Project_Scope.md + _meta/Identify/01_Problem_Definition_Identify.md
- Interact with you (short Q&A)
- Output (Vietnamese): 02_Problem_Definition/Problem_Definition.md

### Step 3 — Create requirements
Ask the agent to:
- Read:
  - Agent_Rules.md
  - Project_Scope.md
  - Problem_Definition.md
  - _meta/Identify/02_Requirements_Identify.md
  - _meta/Checklist/Requirements_Checklist.md
- Interact only if critical requirements info is missing
- Output (Vietnamese): 03_Requirements/Requirements.md
- Include at the end: "Requirements Health Summary" (PASS/PARTIAL/FAIL + top actions)

Example (concept)
To identify requirements, the agent must ground on:
- Project_Scope.md + Problem_Definition.md
And must follow:
- _meta/Identify/02_Requirements_Identify.md + _meta/Checklist/Requirements_Checklist.md
Under:
- Agent_Rules.md

### Step 4 — Create architecture
Ask the agent to:
- Read:
  - Agent_Rules.md
  - Project_Scope.md
  - Problem_Definition.md
  - Requirements.md
  - _meta/Identify/03_Architecture_Identify.md
  - _meta/Checklist/Architecture_Checklist.md
- Interact only if blockers/unknowns exist
- Output (Vietnamese): 04_Architecture/Architecture.md
- Include at the end: "Architecture Health Summary" (PASS/PARTIAL/FAIL + top risks)

### Step 5 — Create detailed design (per Major Block)
Ask the agent to:
- Read: Architecture.md (identify Major Blocks)
- For each Major Block: create 05_Detailed_Design/{MajorBlockName}.md
- Cross-cutting concerns: update 05_Detailed_Design/_overview.md
- This step bridges HLD → Implementation

---

## 2) During development (each work cycle)

Before major work sessions, ask the agent to:
- Read: Agent_Rules.md + _meta/Identify/04_Change_Review.md
- Run triggers (2-of-5 rule)
- Decide which outputs need updates first:
  - 01_Project_Scope/ / 02_Problem_Definition/ / 03_Requirements/ / 04_Architecture/

Rule:
- If 04_Change_Review triggers an update, update docs first (or in the same session) before continuing.

After each work session with code/doc changes:
- Append a summary entry to `09_Changes_History/changes_YYYY-MM-DD.md` (what changed, why).
- If change is later fully reverted/abandoned, remove its entry from the file.
- If a new sub-feature was implemented, update `07_Features/<Area>.md` (add row + status).
- If a new area was created, also add entry to `07_Features/_tracker.md`.
- If deep research/analysis was performed, store outputs in `06_Research/` or `06_Research/analysis/`.

---

## 3) Working modes (how to ask the agent)

Always start by telling the agent to follow Agent_Rules.md.
The agent will declare `Task type: ...` and route to the right module automatically.

### A) Understanding a request (anti-hallucination)
Use when requirements are unclear:
- Module: _meta/Rules/rules/C_requirement_understanding.md

### B) Bug/issue triage
Use when debugging:
- Module: _meta/Rules/rules/B_bug_triage.md
Note: agent must not edit code unless explicitly instructed.

### C) Implementation planning
Use before coding:
- Module: _meta/Rules/rules/E_implementation_plan.md
If a major decision appears, also:
- _meta/Rules/rules/I_adr_lite.md
If delivery risk exists, also:
- _meta/Rules/rules/J_delivery_ops_lite.md

### D) Execute / coding
Use only when you explicitly instruct the agent to implement:
- Module: _meta/Rules/rules/F_execute.md

### E) Update docs and histories
After meaningful changes:
- Module: _meta/Rules/rules/G_docs_histories_update.md

### F) Research "What & Why"
Use only when @docs/@histories/codebase are insufficient:
- Module: _meta/Rules/rules/H_research_what_why.md

---

## 4) Minimal operating rule (1 sentence)

If you only remember one rule:
- Follow Agent_Rules.md, create outputs in order (01 → 02 → 03 → 04 → 05), and use 04_Change_Review.md triggers to decide when to update.
