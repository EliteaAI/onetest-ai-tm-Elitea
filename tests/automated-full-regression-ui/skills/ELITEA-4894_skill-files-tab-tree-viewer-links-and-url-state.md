---
id: ELITEA-4894
title: "Skill Files tab: tree, file viewer and menus, Instructions beside the file, SKILL.md links, and URL state after reload"
priority: critical
type: regression
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7573]
---

# ELITEA-4894: Skill Files tab: tree, file viewer and menus, Instructions beside the file, SKILL.md links, and URL state after reload

**Module:** skills · **Priority:** critical · **Type:** regression

**Objective:** Verify the Files tab basics: the count and the tree, the text and binary viewers, the file and folder menus, the Instructions panel beside a file with link navigation and highlighting, the state kept in the URL after a reload, and the empty state.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill A `regression-skill-files` exists and is saved, with the Instructions and files from Test Data. If the files are missing, add them in **Files → +** (Add files).
- Skill B `regression-skill-nofiles` exists and is saved, with no files.
- Neither skill has unsaved changes.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Skill A | `regression-skill-files` |
| Skill A files | `references/guide.md` (text), `scripts/run.py` (text), `assets/logo.png` (binary), `README.txt` (root) |
| Skill B | `regression-skill-nofiles` (no files) |

Skill A Instructions body:

~~~markdown
# Files skill
See references/guide.md for details.
Run scripts/run.py when needed.
Open [the guide](references/guide.md).
~~~

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Skill A and check the Files card under the Instructions | "Files: Assets 1 · References 1 · Scripts 1 · Other 1" with `Open Files` is shown |
| 2 | Click `Open Files` | `Files – 4` is active. The folders `assets`, `references` and `scripts` are listed before `README.txt` |
| 3 | Click `guide.md`, then `logo.png` | `guide.md` opens read-only with line numbers, with `Instructions` and `Test` in its header. `logo.png` shows "Binary file · … The agent can pass it to a script, not read it." and `Download` |
| 4 | Open the ⋮ menu of a file, then of a folder. Do not run any action | File: `Rename`, `Replace with upload…`, `Download`, `Copy path`, `Delete`. Folder: `Rename folder`, `Upload here`, `Delete folder` |
| 5 | Open `guide.md`, then click `Instructions` | The Instructions open beside the file with Copy, a divider and ✕. The line `See references/guide.md for details.` is highlighted |
| 6 | In the panel, Ctrl-click (⌘-click on macOS) `scripts/run.py` | `run.py` opens, and the highlight moves to its line |
| 7 | Reload the page | The URL keeps `view=files`, `file=scripts%2Frun.py` and `panel=instructions`. The same tab, file and panel are restored |
| 8 | Open `Settings` and, in preview, click "the guide" | The Files tab opens with `guide.md` |
| 9 | Open Skill B and click `Files – 0` | "No files yet" with `Upload files` is shown |

---

## Expected Final State

Both skills are unchanged (no file actions were run).

---

## Pass/Fail Criteria

**Pass:**
- All checkpoints above are met.

**Fail:**
- Wrong count or order, a missing menu item, a binary file shown as text.
- A link does not open the file, no highlight, or the state is lost after reload.

---

## Notes

**Source functional tests:** ELITEA-4889, ELITEA-4890, ELITEA-4891 (AC5, AC10–AC12 of EliteaAI/elitea_issues#7573)
**Regression rationale:** The new Files surface, and the links and URL state shared with the Settings tab.
**Selected checkpoints:** count and order; text and binary viewers; menu items; Instructions panel with Copy and highlight; Ctrl-click link; URL restored after reload; empty state.
**Not covered:** the narrow window (ELITEA-4888), the file actions themselves (upload, rename, delete) and the Viewer role.
