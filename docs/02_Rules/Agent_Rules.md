# Agent_Rules (Entry Point)

This document is the single entry point for all agent work. It preserves all legacy rules and adds routing so the agent can apply the correct module automatically.

---

## 0) Core Language Rule (LEGACY - MUST KEEP)

- All Identify/Rules/Checklists are written in English.
- All generated OUTPUT files are written in Vietnamese:
  - 00_Project_Scope.md
  - 01_Problem_Definition.md
  - 02_Requirements.md
  - 03_Architecture.md

---

## 1) Workflow (LEGACY - MUST FOLLOW)

1) Generate 00_Project_Scope.md:
   - Read: 00_Project_Scope_Identify.md
   - Interact with user until DoR is satisfied.

2) Generate 01_Problem_Definition.md:
   - Read: 00_Project_Scope.md + 01_Problem_Definition_Identify.md
   - Interact with user until DoR is satisfied.

3) Generate 02_Requirements.md:
   - Read: 00_Project_Scope.md + 01_Problem_Definition.md + 02_Requirements_Identify.md + Requirements_Checklist.md
   - Interact with user only for missing critical items or unknowns.

4) Generate 03_Architecture.md:
   - Read: 00_Project_Scope.md + 01_Problem_Definition.md + 02_Requirements.md + 03_Architecture_Identify.md + Architecture_Checklist.md
   - Interact with user only for blockers/unknowns.

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

- Before any major work session, read 04_Change_Review.md and run its triggers.
- If triggers indicate update, update the relevant output docs first (or in the same session).
- Maintain a short “Last updated” + “Change summary (1–3 lines)” section at the top of 00/01/02/03 outputs.
- After each work session with code/doc changes, append a summary entry to `07_Changes_history/changes_YYYY-MM-DD.md`:
  - Date + time
  - What changed (files modified, features added/updated)
  - Why (trigger, user request, bug fix)
- Changes History is a **living changelog** (not a full audit log):
  - **Keep:** entries for changes still active/applied in the project.
  - **Remove:** entries for changes that have been fully reverted/abandoned -- they no longer affect the project.
  - Full history is already in git -- no need to duplicate reverted changes in markdown.
- If new doc files/folders are added or the workflow process itself changes, update How_to_use.md accordingly.

---

## 5) Interaction Rule (LEGACY - MUST KEEP)

- Ask at most 5 questions per round.
- Prefer multiple-choice or short-answer questions.
- Stop asking once DoR is met; carry unknowns forward as “Open questions”.

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
| GLOBAL_GROUNDING | /rules/A_global.md |
| BUG_TRIAGE | /rules/B_bug_triage.md |
| REQUIREMENT_UNDERSTANDING | /rules/C_requirement_understanding.md |
| DOC_RECOMMENDATION | /rules/D_doc_recommendation.md |
| IMPLEMENTATION_PLAN | /rules/E_implementation_plan.md |
| EXECUTE | /rules/F_execute.md |
| DOCS_HISTORIES_UPDATE | /rules/G_docs_histories_update.md |
| RESEARCH_WHAT_WHY | /rules/H_research_what_why.md |
| ADR_LITE | /rules/I_adr_lite.md |
| DELIVERY_OPS_LITE | /rules/J_delivery_ops_lite.md |

---

## 8) Mandatory Grounding Rule (NEW, complements legacy)

Before answering, the agent MUST apply /rules/A_global.md to:
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

## 10) Permission Rule (NEW, aligns with legacy “no edit without instruction”)

- The agent MUST NOT modify code or propose patches as “done work” unless the user explicitly instructs to proceed with editing/implementation.
- In triage/planning mode, the agent may describe options and steps, but must not present changes as already applied.

---

## 11) Feature Tracking (NEW)

- Feature tracking lives in `08_Features/`.
- `_tracker.md` = overview table of all feature areas + status.
- Each area has its own file (e.g. `Document_Management.md`, `Chat.md`).
- When implementing a new sub-feature → update the corresponding area file (add row to table, update status).
- When creating a new area → create file + add entry to `_tracker.md`.
- Status icons: ✅ Done | 🔧 In Progress | ⬜ TBD | ❌ Removed/Legacy.
- Area maps to FR-xx in Requirements (FR-02 → Contracts, FR-04 → Document_Management, etc.).

---

## 12) Extension Rules (NEW)

To keep PoC/Spike projects lightweight, specialized rules are placed in `02_Rules/extensions/`. The agent MUST dynamically apply these based on `04_Prerequisites/00_Project_Scope.md`:

- If **Scale** = "Production" OR **Scale** = "MVP/Feature", the agent MUST read `02_Rules/extensions/ext_coding_conventions.md` before executing any code changes.
- If **Scale** = "Production", the agent MUST read `02_Rules/extensions/ext_testing_strategy.md`.
- If **Constraints** mentions "Security", "Compliance", or if data sensitivity is high, the agent MUST read `02_Rules/extensions/ext_security_audit.md`.

*(For PoC or Spike, skip these extensions to save time, unless the user explicitly requests them).*
