# Migration Guide — Sync Project to Latest B34R-e Template

This guide migrates any project's `agent-framework/` from any older version to the latest B34R-e structure.

---

## 0) Detect current version

Check which structure your project uses:

| Check | Version |
|---|---|
| Has `04_Prerequisites/00_Project_Scope.md` | v1 (original flat) |
| Has `01_Project_Scope/Project_Scope.md` + `_meta/` | v2 (current latest) |

If already v2 → skip to **Step 5** (sync control files only).

---

## 1) Create new folder structure

```bash
cd <project>/agent-framework

# Meta (control files)
mkdir -p _meta/README _meta/Rules/rules _meta/Rules/extensions _meta/Identify _meta/Checklist

# SDLC phases
mkdir -p 01_Project_Scope 02_Problem_Definition 03_Requirements 04_Architecture
mkdir -p 05_Detailed_Design
mkdir -p 06_Research/analysis
mkdir -p 07_Features 08_Business_Flow 09_Changes_History 10_Common 11_Environment
```

---

## 2) Move project OUTPUT files (keep content, change location)

These files contain YOUR project data — move them, do NOT overwrite with template.

| Old path (v1) | New path (v2) |
|---|---|
| `04_Prerequisites/00_Project_Scope.md` | `01_Project_Scope/Project_Scope.md` |
| `04_Prerequisites/01_Problem_Definition.md` | `02_Problem_Definition/Problem_Definition.md` |
| `04_Prerequisites/02_Requirements.md` | `03_Requirements/Requirements.md` |
| `04_Prerequisites/03_Architecture.md` | `04_Architecture/Architecture.md` |
| `05_Research/*` | `06_Research/*` |
| `05_Research/analysis/*` (if exists) | `06_Research/analysis/*` |
| `06_Analyze/*` | `06_Research/analysis/*` |
| `07_Changes_history/*` | `09_Changes_History/*` |
| `08_Features/*` | `07_Features/*` |
| `09_Business_Flow/*` | `08_Business_Flow/*` |
| `10_Common/*` | `10_Common/*` (no change) |
| `11_Environment/*` | `11_Environment/*` (no change) |

```bash
# Example commands (adapt to your project):
mv 04_Prerequisites/00_Project_Scope.md 01_Project_Scope/Project_Scope.md
mv 04_Prerequisites/01_Problem_Definition.md 02_Problem_Definition/Problem_Definition.md
mv 04_Prerequisites/02_Requirements.md 03_Requirements/Requirements.md
mv 04_Prerequisites/03_Architecture.md 04_Architecture/Architecture.md

# Research + Analysis merge
mv 05_Research/* 06_Research/ 2>/dev/null
mv 06_Analyze/* 06_Research/analysis/ 2>/dev/null

# History, Features, Business Flow (note: numbers shifted)
mv 07_Changes_history/* 09_Changes_History/ 2>/dev/null
mv 08_Features/* 07_Features/ 2>/dev/null
mv 09_Business_Flow/* 08_Business_Flow/ 2>/dev/null
```

---

## 3) Copy CONTROL files from B34R-e template

These files are the framework engine — always overwrite with latest template version.

```bash
B34R=<path_to_B34R-e>/agent_framework
PROJ=<path_to_project>/agent-framework

# Meta control files (OVERWRITE — these are template-owned)
cp -r $B34R/_meta/Identify/* $PROJ/_meta/Identify/
cp -r $B34R/_meta/Checklist/* $PROJ/_meta/Checklist/
cp -r $B34R/_meta/Rules/* $PROJ/_meta/Rules/
cp -r $B34R/_meta/README/* $PROJ/_meta/README/
cp $B34R/README.md $PROJ/README.md

# New: Detailed Design overview (only if not already customized)
cp -n $B34R/05_Detailed_Design/_overview.md $PROJ/05_Detailed_Design/_overview.md

# New: Environment template (only if not already customized)
cp -n $B34R/11_Environment/SETUP.md $PROJ/11_Environment/SETUP.md
```

**`cp -n`** = do not overwrite if file already exists (preserves project-specific content).

---

## 4) Remove old folders

Only after verifying all files were moved successfully:

```bash
# Remove old structure
rm -rf 04_Prerequisites 05_Research 06_Analyze 07_Changes_history 08_Features 09_Business_Flow
rm -rf 00_Identify 01_Checklist 02_Rules 03_README
```

---

## 5) Update bridge files (if using Claude Code)

If project has `.claude/rules/` bridge files, update references:

| File | Old reference | New reference |
|---|---|---|
| `CLAUDE.md` | `agent-framework/02_Rules/Agent_Rules.md` | `agent-framework/_meta/Rules/Agent_Rules.md` |
| `.claude/rules/development-rules.md` | `agent-framework/02_Rules/Agent_Rules.md` | `agent-framework/_meta/Rules/Agent_Rules.md` |
| `.claude/rules/development-rules.md` | `agent-framework/02_Rules/extensions/...` | `agent-framework/_meta/Rules/extensions/...` |
| `.claude/rules/primary-workflow.md` | `agent-framework/02_Rules/Agent_Rules.md` | `agent-framework/_meta/Rules/Agent_Rules.md` |
| `.claude/rules/documentation-management.md` | `agent-framework/02_Rules/rules/G_...` | `agent-framework/_meta/Rules/rules/G_...` |
| `.claude/rules/documentation-management.md` | `agent-framework/03_README/How_to_use.md` | `agent-framework/_meta/README/How_to_use.md` |

---

## 6) Verify

```bash
# 1. No old references remain
grep -r "04_Prerequisites\|05_Research\|06_Analyze\|07_Changes_history\|08_Features\|00_Identify\|01_Checklist\|02_Rules\|03_README" agent-framework/

# 2. Structure matches template
diff <(cd $B34R && find . -type d | sort) <(cd $PROJ && find . -type d | sort)

# 3. Aliases resolve (read A_global.md, verify each alias path exists)
cat agent-framework/_meta/Rules/rules/A_global.md
```

If grep returns matches → fix those references.
If diff shows differences → missing folders need to be created.

---

## 7) Version history

| Version | Date | Changes |
|---|---|---|
| v1 | 2026-03-08 | Original: 00-11 flat numbered folders, 04_Prerequisites contains all outputs |
| v2 | 2026-03-13 | Meta/SDLC split, Detailed Design added, Analyze merged into Research, numbers realigned |
