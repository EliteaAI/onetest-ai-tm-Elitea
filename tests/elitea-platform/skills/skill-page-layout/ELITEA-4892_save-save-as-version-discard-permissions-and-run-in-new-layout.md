---
id: ELITEA-4892
title: "Save, Save As Version, Discard, permissions and runs work as before in the new skill page layout"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7573]
---

# ELITEA-4892: Save, Save As Version, Discard, permissions and runs work as before in the new skill page layout

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that the new layout keeps Save, Save As Version, Discard, permissions and the run behaviour as they were.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill A `layout-skill` exists and is saved, with the Instructions and files from Test Data. If the files are missing, add them in **Files → +** (Add files).
- Skill B `layout-skill-empty` exists and is saved, with no files.
- The browser window is at least 1366 × 768 px, unless a step says otherwise.
- A Viewer user exists in the same project, and Skill A has a published version.

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
| 1 | Change the Description, add `LAYOUT-MARKER` in `</>`, click `Save`, then reload | The toast "Skill saved" appears. Both changes are kept after reload |
| 2 | Add more text and click `Discard` | The dialog "Warning — Are you sure you want to discard changes?" with `Cancel` and `Discard` appears. After confirming, only the new text is removed |
| 3 | Click `Save As Version`, enter `layout-v2` in "Create version" and click `Save` | `VERSION: layout-v2` opens with the same Instructions and `Files – 4` |
| 4 | Click `Test` and send `hello` | The reply contains `LAYOUT-OK`. The "Testing unsaved changes" banner is not shown. The URL gets `run=<id>` |
| 5 | Log in as the Viewer and open Skill A in both tabs, then open its published version | Save, Save As Version and Discard are hidden or disabled. The Instructions are read-only. File menus show only `Download` and `Copy path`. There is no "+" (Add files) and no folder menu |
| 6 | As the Editor, delete version `layout-v2` and restore the original Description | Skill A is back to its original state |

---

## Expected Final State

Skill A has only its original versions and description.

---

## Pass/Fail Criteria

**Pass:**
- Save, Discard and Save As Version work as before, and the new version keeps the files.
- Test runs on the open version.
- Viewer and published versions are read-only.

**Fail:**
- Any of these actions fails or behaves differently than before.
- A Viewer can edit, save or change files.

---

## Notes

- Covers AC13 of EliteaAI/elitea_issues#7573. Detailed coverage: ELITEA-4747 (versions, Discard), ELITEA-4748 (Viewer), ELITEA-2440 (Test uses the selected version).
- Steps 1–4 verified on DEV against EliteaUI#1575 on 2026-11-25. Step 5 (Viewer, published version) was not verified: no Viewer account was available.
