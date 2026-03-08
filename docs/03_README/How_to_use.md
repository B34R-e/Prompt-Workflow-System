# How_to_use.md

This document explains how to use the agent docs in a short, practical way.

---

## 0) What is what

### OUTPUT files (Vietnamese)
These are the deliverables you maintain per project, stored in `04_Prerequisites/`:
- 04_Prerequisites/00_Project_Scope.md
- 04_Prerequisites/01_Problem_Definition.md
- 04_Prerequisites/02_Requirements.md
- 04_Prerequisites/03_Architecture.md

### CONTROL files (English)
These guide the agent on how to produce / update the outputs:
- Agent_Rules.md (entry point + routing)
- 00_Project_Scope_Identify.md
- 01_Problem_Definition_Identify.md
- 02_Requirements_Identify.md
- 03_Architecture_Identify.md
- 04_Change_Review.md
- Requirements_Checklist.md
- Architecture_Checklist.md
- /rules/A_global.md … /rules/J_delivery_ops_lite.md
- **/extensions/**: Conditional rules dynamically loaded for Production/MVP scale (e.g. `ext_coding_conventions.md`, `ext_testing_strategy.md`, `ext_security_audit.md`).

### HISTORY files
Living changelog — only active/applied changes, reverted ones are removed:
- 07_Changes_history/changes_YYYY-MM-DD.md

### FEATURE TRACKING files (Vietnamese)
Per-area feature tracking — monitor sub-features and status:
- 08_Features/_tracker.md (overview table)
- 08_Features/Contracts.md, Sessions.md, Document_Management.md, Chat.md, Members.md

---

## 1) Start a new project (initialization)

### Step 1 — Create scope
Ask the agent to:
- Read: Agent_Rules.md + 00_Project_Scope_Identify.md
- Interact with you (short Q&A)
- Output (Vietnamese): 04_Prerequisites/00_Project_Scope.md

### Step 2 — Create problem definition
Ask the agent to:
- Read: Agent_Rules.md + 00_Project_Scope.md + 01_Problem_Definition_Identify.md
- Interact with you (short Q&A)
- Output (Vietnamese): 04_Prerequisites/01_Problem_Definition.md

### Step 3 — Create requirements
Ask the agent to:
- Read:
  - Agent_Rules.md
  - 00_Project_Scope.md
  - 01_Problem_Definition.md
  - 02_Requirements_Identify.md
  - Requirements_Checklist.md
- Interact only if critical requirements info is missing
- Output (Vietnamese): 04_Prerequisites/02_Requirements.md
- Include at the end: “Requirements Health Summary” (PASS/PARTIAL/FAIL + top actions)

Example (concept)
To identify requirements, the agent must ground on:
- 00_Project_Scope.md + 01_Problem_Definition.md
And must follow:
- 02_Requirements_Identify.md + Requirements_Checklist.md
Under:
- Agent_Rules.md

### Step 4 — Create architecture
Ask the agent to:
- Read:
  - Agent_Rules.md
  - 00_Project_Scope.md
  - 01_Problem_Definition.md
  - 02_Requirements.md
  - 03_Architecture_Identify.md
  - Architecture_Checklist.md
- Interact only if blockers/unknowns exist
- Output (Vietnamese): 04_Prerequisites/03_Architecture.md
- Include at the end: “Architecture Health Summary” (PASS/PARTIAL/FAIL + top risks)

---

## 2) During development (each work cycle)

Before major work sessions, ask the agent to:
- Read: Agent_Rules.md + 04_Change_Review.md
- Run triggers (2-of-5 rule)
- Decide which outputs need updates first:
  - 04_Prerequisites/00_Project_Scope.md / 04_Prerequisites/01_Problem_Definition.md / 04_Prerequisites/02_Requirements.md / 04_Prerequisites/03_Architecture.md

Rule:
- If 04_Change_Review triggers an update, update docs first (or in the same session) before continuing.

After each work session with code/doc changes:
- Append a summary entry to `07_Changes_history/changes_YYYY-MM-DD.md` (what changed, why).
- If change is later fully reverted/abandoned, remove its entry from the file.
- If a new sub-feature was implemented, update `08_Features/<Area>.md` (add row + status).
- If a new area was created, also add entry to `08_Features/_tracker.md`.

---

## 3) Working modes (how to ask the agent)

Always start by telling the agent to follow Agent_Rules.md.  
The agent will declare `Task type: ...` and route to the right module automatically.

### A) Understanding a request (anti-hallucination)
Use when requirements are unclear:
- Module: /rules/C_requirement_understanding.md

### B) Bug/issue triage
Use when debugging:
- Module: /rules/B_bug_triage.md
Note: agent must not edit code unless explicitly instructed.

### C) Implementation planning
Use before coding:
- Module: /rules/E_implementation_plan.md
If a major decision appears, also:
- /rules/I_adr_lite.md
If delivery risk exists, also:
- /rules/J_delivery_ops_lite.md

### D) Execute / coding
Use only when you explicitly instruct the agent to implement:
- Module: /rules/F_execute.md

### E) Update docs and histories
After meaningful changes:
- Module: /rules/G_docs_histories_update.md

### F) Research “What & Why”
Use only when @docs/@histories/codebase are insufficient:
- Module: /rules/H_research_what_why.md

---

## 4) Minimal operating rule (1 sentence)

If you only remember one rule:
- Follow Agent_Rules.md, create outputs in order (00 → 01 → 02 → 03), and use 04_Change_Review.md triggers to decide when to update.
