---
id: ELITEA-4889
title: "Files tab shows the count, the tree with folders first, the file viewer, the file and folder menus, the Files card and the empty state"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7573]
---

# ELITEA-4889: Files tab shows the count, the tree with folders first, the file viewer, the file and folder menus, the Files card and the empty state

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify the Files tab basics: the file count in the tab, folders listed before files, a file opening on click (text read-only with line numbers, binary as a Download card), the items of the file and folder menus, the Files card on Settings, and the empty state of a skill with no files.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill A `layout-skill` exists and is saved, with the Instructions and files from Test Data. If the files are missing, add them in **Files → +** (Add files).
- Skill B `layout-skill-empty` exists and is saved, with no files.
- The browser window is at least 1366 × 768 px, unless a step says otherwise.

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Skill A | `layout-skill` |
| Skill A files | `references/guide.md` (text, 3 lines), `scripts/run.py` (text), `assets/logo.png` (binary), `README.txt` (root) |
| Skill B | `layout-skill-empty` (no files) |
| Marker | `LAYOUT-MARKER` |

Skill A Instructions body:

~~~markdown
# Layout test skill

See references/guide.md for details.
Run scripts/run.py when needed.
Open [the guide](references/guide.md).

Reply with LAYOUT-OK.
~~~

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Skill A and click `Files – 4` | The tree lists the folders `assets`, `references` and `scripts` (each with its file) before the root file `README.txt`. A "+" (Add files) button is in the tab bar |
| 2 | Click `guide.md` | The header shows `guide.md`, `Instructions`, `Test` and a link icon ("Copy the file path to paste into the instructions"). The content is read-only with line numbers. The URL has `view=files&file=references%2Fguide.md` |
| 3 | Click `logo.png` | A card shows "Binary file · 70 Bytes. The agent can pass it to a script, not read it." and `Download` |
| 4 | Open the ⋮ (More) menu of a file, then of a folder. Do not run any action | File menu: `Rename`, `Replace with upload…`, `Download`, `Copy path`, `Delete`. Folder menu: `Rename folder`, `Upload here`, `Delete folder` |
| 5 | Open `Settings` and check under the Instructions | The card reads "Files: Assets 1 · References 1 · Scripts 1 · Other 1" with `Open Files`. `Open Files` opens the Files tab |
| 6 | Open Skill B and click `Files – 0` | "No files yet" with `Upload files` is shown. No errors |

---

## Expected Final State

Both skills are unchanged (no file actions were run).

---

## Pass/Fail Criteria

**Pass:**
- Count, order, viewers, menus, Files card and empty state are as described.

**Fail:**
- Wrong count or order, a file does not open, a binary file is shown as text.
- A menu item is missing or extra.
- No empty state for a skill without files.

---

## Notes

- Covers AC10 of EliteaAI/elitea_issues#7573. Only the menu items are checked; the file actions themselves are not run.
- Steps verified on DEV against EliteaUI#1575 on 2026-11-25.
