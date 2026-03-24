# B34R-e Upgrade Plan

> Current score: 90.8/100 | Target: 93.5/100
> Created: 2026-03-10

---

## Phase 1 — Consistency (84 → 90) | Effort: Low

### 1.1 Renumber How_to_use.md sections
- File: `agent_framework/03_README/How_to_use.md`
- Change: "0)" → "1)", "0.5)" → "2)", "1)" → "3)", etc. Setup comes before "What is what"
- Why: Fractional numbering breaks pattern recognition for both human and LLM

### 1.2 Remove emoji from Agent_Rules.md Section 11
- File: `agent_framework/02_Rules/Agent_Rules.md`
- Change: Replace ✅🔧⬜❌ with text labels (Done / In Progress / TBD / Removed)
- Why: All other modules use pure text — mixed convention confuses agent on which is standard

### 1.3 Add missing aliases to A_global.md
- File: `agent_framework/02_Rules/rules/A_global.md`
- Change: Add `@research = 05_Research/` and `@analysis = 06_Analyze/`
- Why: H_research_what_why.md references these folders without alias — violates own centralization principle

### 1.4 Normalize README.md emoji usage
- File: `agent_framework/README.md`
- Change: Remove emoji from headers (keep professional for sellable framework)
- Why: README uses emoji headers, no other file does — inconsistent

---

## Phase 2 — Onboarding (85 → 92) | Effort: Low-Medium

### 2.1 Reorder How_to_use.md: Setup first
- File: `agent_framework/03_README/How_to_use.md`
- Change: Move setup section before "What is what" section
- Why: Instructional design — user must have folder in project before understanding file roles

### 2.2 Create Glossary
- File: `agent_framework/03_README/Glossary.md` (NEW)
- Content: 15-20 terms — DoR, @docs, @histories, @features, @research, @analysis, Living changelog, 2-of-5 rule, Extension, Bridge Pattern, Task type, Module, Scale levels, Evidence format, Assumption vs Unknown
- Why: O(1) term lookup vs O(n) cross-file search. Reduces agent backtracking

### 2.3 Add .gitkeep with purpose comments to empty folders
- Folders: `04_Prerequisites/`, `05_Research/`, `06_Analyze/`, `07_Changes_history/`, `08_Features/`, `09_Business_Flow/`, `10_Common/`
- Content per .gitkeep: `# Purpose: <one-line description from How_to_use.md>`
- Why: Empty folder = zero signal for agent using `ls`. 1-line purpose = instant understanding

---

## Phase 3 — Content Depth (88 → 93) | Effort: Medium

### 3.1 Expand ext_coding_conventions.md
- File: `agent_framework/02_Rules/extensions/ext_coding_conventions.md`
- Change: Add "How to apply" section with per-tech-stack examples (TypeScript, C#, Python)
- Target: 14 → ~40 lines
- Why: Current rules are Bloom's level 1 (remember). Need level 3 (apply) with concrete examples

### 3.2 Expand ext_testing_strategy.md
- File: `agent_framework/02_Rules/extensions/ext_testing_strategy.md`
- Change: Add test pyramid guidance, specify coverage metric type (line/branch/function), mock vs real criteria
- Target: 14 → ~40 lines
- Why: "80% coverage" without specifying metric type is ambiguous — agent picks easiest (line) which is least useful

### 3.3 Expand ext_security_audit.md
- File: `agent_framework/02_Rules/extensions/ext_security_audit.md`
- Change: Map rules to OWASP Top 10. Add missing: broken access control (#1), security misconfiguration (#5), SSRF (#10)
- Target: 14 → ~40 lines
- Why: Current 6/10 OWASP coverage leaves gaps in the 3 most critical categories

### 3.4 Create K_code_review.md module
- File: `agent_framework/02_Rules/rules/K_code_review.md` (NEW)
- Also update: `Agent_Rules.md` Section 6 (add CODE_REVIEW type), Section 7 (routing), Section 9 (composition)
- Content: Purpose, when to use, output format (what to check, severity, approve/request-changes), rules
- Why: Has BUG_TRIAGE (reactive) but no CODE_REVIEW (preventive). Code Complete Ch.21: formal inspections catch 60% of defects

---

## Phase 4 — Extensibility (90 → 94) | Effort: Low

### 4.1 Add "How to extend" section to How_to_use.md
- File: `agent_framework/03_README/How_to_use.md`
- Content: Step-by-step guide to add new module, new extension, new folder
- Why: Open-Closed Principle for docs — extensible without reading all source files

### 4.2 Create Quick Reference Card
- File: `agent_framework/03_README/Quick_Reference.md` (NEW)
- Content: ~30 lines — routing table, aliases, conventions, file categories
- Why: Token efficiency — Agent_Rules.md 168 lines, but 90% of lookups need only 30 lines of info

---

## Execution Notes

- Phase 1-2: Do in 1 session (~30 min). Low risk, high consistency impact.
- Phase 3-4: Do incrementally when encountering real pain points from projects.
- After all phases: Re-evaluate. Target 93.5 is sweet spot — beyond that is over-engineering (violates YAGNI).
- After updating B34R-e template, sync changes to any active projects using it (e.g., Proj4's `agent-framework/agent_framework/`).
