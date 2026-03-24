# Agent_Rules (Entry Point)

This document is the single entry point for all agent work. It preserves all legacy rules and adds routing so the agent can apply the correct module automatically.

---

## 0) Core Language Rule (LEGACY - MUST KEEP)

- All Identify/Rules/Checklists are written in English (stored in `_meta/`).
- All generated OUTPUT files are written in Vietnamese:
  - 01_Project_Scope/Project_Scope.md
  - 02_Problem_Definition/Problem_Definition.md
  - 03_Requirements/Requirements.md
  - 04_Architecture/Architecture.md
  - 05_Detailed_Design/{MajorBlockName}.md

---

## 1) Workflow (LEGACY - MUST FOLLOW)

1) Generate Project_Scope.md:
   - Read: _meta/Identify/00_Project_Scope_Identify.md
   - Interact with user until DoR is satisfied.
   - Output: 01_Project_Scope/Project_Scope.md

2) Generate Problem_Definition.md:
   - Read: Project_Scope.md + _meta/Identify/01_Problem_Definition_Identify.md
   - Interact with user until DoR is satisfied.
   - Output: 02_Problem_Definition/Problem_Definition.md

3) Generate Requirements.md:
   - Read: Project_Scope.md + Problem_Definition.md + _meta/Identify/02_Requirements_Identify.md + _meta/Checklist/Requirements_Checklist.md
   - Interact with user only for missing critical items or unknowns.
   - Output: 03_Requirements/Requirements.md

4) Generate Architecture.md:
   - Read: Project_Scope.md + Problem_Definition.md + Requirements.md + _meta/Identify/03_Architecture_Identify.md + _meta/Checklist/Architecture_Checklist.md
   - Interact with user only for blockers/unknowns.
   - Output: 04_Architecture/Architecture.md

5) Generate Detailed Design (per Major Block):
   - Read: Architecture.md (identify Major Blocks)
   - For each Major Block: create 05_Detailed_Design/{MajorBlockName}.md
   - Define: classes, methods, data flow, error handling, dependencies
   - Cross-cutting concerns go in 05_Detailed_Design/_overview.md

---

## 2) Writing Principles (LEGACY - MUST KEEP)

- Minimal but sufficient: write only what is needed to enable construction and review.
- Checklist-driven expansion: add detail only when checklist items are PARTIAL/FAIL.
- No guessing: record unknowns explicitly; ask targeted questions only when blocking.
- Avoid design in requirements: requirements describe what; architecture describes how at a high level.
- Apply 80/20 in architecture: cover critical classes/components first.

---

## 3) Length Guidance (LEGACY - MUST KEEP)

- PoC/Spike: ~0.5–1.5 pages per output file
- MVP/Feature: ~1–3 pages per output file
- Production/Scale: ~3–7 pages per output file (more only for compliance)

---

## 4) Change Management (LEGACY - MUST KEEP)

- Before any major work session, read _meta/Identify/04_Change_Review.md and run its triggers.
- If triggers indicate update, update the relevant output docs first (or in the same session).
- Maintain a short "Last updated" + "Change summary (1–3 lines)" section at the top of output files.
- After each work session with code/doc changes, append a summary entry to `09_Changes_History/changes_YYYY-MM-DD.md`:
  - Date + time
  - What changed (files modified, features added/updated)
  - Why (trigger, user request, bug fix)
- Changes History is a **living changelog** (not a full audit log):
  - **Keep:** entries for changes still active/applied in the project.
  - **Remove:** entries for changes that have been fully reverted/abandoned -- they no longer affect the project.
  - Full history is already in git -- no need to duplicate reverted changes in markdown.
- If new doc files/folders are added or the workflow process itself changes, update _meta/README/How_to_use.md accordingly.

---

## 5) Interaction Rule (LEGACY - MUST KEEP)

- Ask at most 5 questions per round.
- Prefer multiple-choice or short-answer questions.
- Stop asking once DoR is met; carry unknowns forward as "Open questions".

---

## 6) Task Type Declaration (NEW - REQUIRED)

Every response MUST begin with:
- Task type: <ONE OF the types below>

Valid task types (router keys):
- GLOBAL_GROUNDING
- BUG_TRIAGE
- REQUIREMENT_UNDERSTANDING
- DOC_RECOMMENDATION
- IMPLEMENTATION_PLAN
- EXECUTE
- DOCS_HISTORIES_UPDATE
- RESEARCH_WHAT_WHY
- ADR_LITE
- DELIVERY_OPS_LITE

---

## 7) Routing Table (NEW)

The agent MUST select the module(s) below based on the user's request.

| Task type | Use module file |
|---|---|
| GLOBAL_GROUNDING | _meta/Rules/rules/A_global.md |
| BUG_TRIAGE | _meta/Rules/rules/B_bug_triage.md |
| REQUIREMENT_UNDERSTANDING | _meta/Rules/rules/C_requirement_understanding.md |
| DOC_RECOMMENDATION | _meta/Rules/rules/D_doc_recommendation.md |
| IMPLEMENTATION_PLAN | _meta/Rules/rules/E_implementation_plan.md |
| EXECUTE | _meta/Rules/rules/F_execute.md |
| DOCS_HISTORIES_UPDATE | _meta/Rules/rules/G_docs_histories_update.md |
| RESEARCH_WHAT_WHY | _meta/Rules/rules/H_research_what_why.md |
| ADR_LITE | _meta/Rules/rules/I_adr_lite.md |
| DELIVERY_OPS_LITE | _meta/Rules/rules/J_delivery_ops_lite.md |

---

## 8) Mandatory Grounding Rule (NEW, complements legacy)

Before answering, the agent MUST apply _meta/Rules/rules/A_global.md to:
- choose sources in priority order,
- label evidence vs assumption vs unknown,
- avoid over-engineering.

This is required even when another module is used.

---

## 9) Module Composition Rule (NEW)

Some tasks must chain modules:

- If implementing changes: E_implementation_plan → (I_adr_lite if major decision) → (J_delivery_ops_lite if delivery risk) → F_execute → G_docs_histories_update
- If unclear requirements: C_requirement_understanding → (H_research_what_why only if needed) → E_implementation_plan
- If bug: B_bug_triage → E_implementation_plan (if requested) → F_execute (only when explicitly instructed)

---

## 10) Permission Rule (NEW, aligns with legacy "no edit without instruction")

**This rule applies to ALL modules and ALL task types — not just EXECUTE.**

- The agent MUST NOT modify code, files, or propose patches as "done work" unless the user explicitly instructs to proceed with editing/implementation.
- In triage/planning mode, the agent may describe options and steps, but must not present changes as already applied.
- Explicit permission means one of:
  - User says "proceed", "go ahead", "do it", "implement", "fix it", or equivalent
  - User selects a proposed approach and instructs to execute
- If unclear whether user wants execution or just analysis: default to analysis and ask.
- Violation of this rule = agent must stop, undo if possible, and re-confirm with user.

---

## 11) Feature Tracking (NEW)

- Feature tracking lives in `07_Features/`.
- `_tracker.md` = overview table of all feature areas + status.
- Each area has its own file (e.g. `Document_Management.md`, `Chat.md`).
- When implementing a new sub-feature → update the corresponding area file (add row to table, update status).
- When creating a new area → create file + add entry to `_tracker.md`.
- Status icons: ✅ Done | 🔧 In Progress | ⬜ TBD | ❌ Removed/Legacy.
- Area maps to FR-xx in Requirements (FR-02 → Contracts, FR-04 → Document_Management, etc.).

---

## 12) Extension Rules (NEW)

To keep PoC/Spike projects lightweight, specialized rules are placed in `_meta/Rules/extensions/`. The agent MUST dynamically apply these based on `01_Project_Scope/Project_Scope.md`:

- If **Scale** = "Production" OR **Scale** = "MVP/Feature", the agent MUST read `_meta/Rules/extensions/ext_coding_conventions.md` before executing any code changes.
- If **Scale** = "Production", the agent MUST read `_meta/Rules/extensions/ext_testing_strategy.md`.
- If **Constraints** mentions "Security", "Compliance", or if data sensitivity is high, the agent MUST read `_meta/Rules/extensions/ext_security_audit.md`.

*(For PoC or Spike, skip these extensions to save time, unless the user explicitly requests them).*

---

## 13) Output Routing Map (NEW)

When creating or updating documentation, the agent MUST place files in the correct folder based on content type:

| Content type | Target folder | Examples |
|---|---|---|
| Project scope, vision, constraints | `01_Project_Scope/` | Project_Scope.md |
| Problem statement, stakeholders | `02_Problem_Definition/` | Problem_Definition.md |
| Functional & non-functional requirements | `03_Requirements/` | Requirements.md |
| High-level design, major blocks, interfaces | `04_Architecture/` | Architecture.md |
| Per-block detailed design (classes, methods, data flow) | `05_Detailed_Design/` | {MajorBlockName}.md |
| Research notes, deep dives, comparisons | `06_Research/` | topic-name.md |
| Analysis documents, implementation plans | `06_Research/analysis/` | analysis-topic.md |
| Feature area tracking (status, sub-features) | `07_Features/` | _tracker.md, {Area}.md |
| Business process flows, user journeys | `08_Business_Flow/` | process-name.md |
| Changelog entries | `09_Changes_History/` | changes_YYYY-MM-DD.md |
| API specs, DB schema, security refs, monitoring URLs | `10_Common/` | API_Reference.md, Monitoring.md |
| Setup guides, deployment guides, Runbook, config refs | `11_Environment/` | SETUP.md, Runbook.md, Deploy_Guide.md |

**Rule:** If content does not match any row above, ask the user where to place it. Do NOT create files outside the framework structure without explicit instruction.

---

## 14) Understanding Confirmation Gate (NEW)

Before proceeding with any task, the agent MUST follow this sequence:

1. **Restate understanding**: summarize what is being asked (scope, intent, constraints) in concise bullets
2. **Propose recommendations**: 2–3 approaches, each with:
   - What: brief description of the approach
   - Why: explicit rationale for choosing this approach (trade-offs, pros/cons)
   - Success estimate: X% likelihood of success + explanation (based on complexity, known risks, dependencies, evidence quality)
   - Impact: what changes, what risks
3. **Ask grounding source**: "Do you want this grounded by a specific source?" (e.g., existing docs, codebase, MCP context7, external research)
4. **Wait for explicit user selection**: do NOT proceed until user picks an approach or gives go-ahead
   - If user proposes their own approach: the agent MUST also evaluate it with the same format (What / Why / Success estimate / Impact) before proceeding
5. **Confirm before execute**: after user selects, restate the chosen approach and ask "Proceed?" before making any changes

This applies to ALL task types. If the user's intent is ambiguous, ask clarifying questions instead of assuming.

Exception: trivial/obvious tasks (e.g., "read file X", "show me file Y") may skip this gate.

**Violation**: if the agent skips this gate and proceeds directly → it must stop, explain what it did, and re-confirm with user.
