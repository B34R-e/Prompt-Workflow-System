# Breaking Changes Update Rules

Purpose
- Ensure all path references stay consistent when folder structure changes (rename, move, add, remove).
- Minimize update surface: path knowledge is centralized, not scattered.

---

## 1) Where paths live (update targets)

Only these files contain path references. When structure changes, update ONLY these:

| File | What it contains | Update when |
|---|---|---|
| `_meta/Rules/rules/A_global.md` → Folder aliases | `@docs`, `@histories`, `@features` → actual folder paths | Folder renamed/renumbered/removed |
| `_meta/README/How_to_use.md` → Section 0 | Full inventory of all folders + files with paths | Any structural change |
| `_meta/Rules/Agent_Rules.md` | Sparse path references (e.g. `_meta/README/How_to_use.md`) | Only if a referenced file moves |
| `README.md` (framework root) | Folder structure description for onboarding | Folder added/removed/renamed |

---

## 2) Update order

When a structural change happens, update in this order:

1. **A_global.md aliases first** — all modules inherit from here. If aliases are wrong, every module breaks.
2. **How_to_use.md Section 0** — human reference, must match filesystem.
3. **Agent_Rules.md** — only if it directly references a moved/renamed path.
4. **README.md** — last, it's onboarding context not agent-critical.

---

## 3) Rules per change type

### Folder renamed or renumbered
- Update A_global.md aliases (if the folder has an alias).
- Update How_to_use.md Section 0 inventory.
- Grep the framework root for the old folder name → fix any remaining references.

### New folder added
- Add entry to How_to_use.md Section 0 under the correct category.
- If the folder will be referenced by rule modules, add an alias in A_global.md.
- If not referenced by modules (scratchpad/reference), no alias needed.

### Folder removed or merged
- Remove/update alias in A_global.md (if exists).
- Remove/update entry in How_to_use.md Section 0.
- Grep the framework root for the old folder name → remove or redirect references.

### File moved between folders
- If the file is listed in How_to_use.md Section 0, update the path there.
- If Agent_Rules.md references it by path, update there.
- No alias change needed (aliases point to folders, not files).

### New file added to existing folder
- If the file is a new CONTROL file (Identify/Checklist/Rule), add to How_to_use.md Section 0 CONTROL list.
- If the file is a new output/tracking file, add to the relevant category in How_to_use.md Section 0.

---

## 4) Verification

After updating, run this check:
- List all folders in the framework root → compare against How_to_use.md Section 0. Every folder must appear.
- Read A_global.md aliases → verify each alias path exists on filesystem.
- If discrepancy found: fix immediately before continuing other work.

---

## 5) What NOT to do

- Do NOT add full paths inside individual rule modules (`_meta/Rules/rules/*.md`). They use aliases from A_global.md.
- Do NOT duplicate folder structure in multiple files. How_to_use.md Section 0 is the single inventory.
- Do NOT create aliases for folders that no module references. Aliases are for write targets, not for every folder.
