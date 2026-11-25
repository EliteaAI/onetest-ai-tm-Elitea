---
id: ELITEA-4887
title: "Test opens as a third column without starting a run; Full screen and close keep edits and the test chat"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7573]
---

# ELITEA-4887: Test opens as a third column without starting a run; Full screen and close keep edits and the test chat

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that Test opens as a third column on the right without starting a run, Full screen of Test hides the other columns, and closing and reopening Test keeps the unsaved edits and the test chat.

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
| 1 | Open Skill A, click `</>` and add `LAYOUT-MARKER`. Do not save | `Save` is enabled |
| 2 | Click `Test` in the Instructions header | A `Test` column opens on the right, about a third of the window wide. Its header has Fullscreen mode, clear the chat, view run history and ✕. The banner "Testing unsaved changes — this run is not saved to history" is shown. No message is sent. The URL gets `panel=test` |
| 3 | Send `hello` | The reply contains `LAYOUT-OK`. No errors |
| 4 | Click Fullscreen mode, then Exit fullscreen mode | In full screen the Settings and Instructions columns are hidden. After exit both come back and `LAYOUT-MARKER` is still in the editor |
| 5 | Click ✕ ("Close"), then `Test` again | The column closes and `panel=test` leaves the URL. After reopening, the earlier `hello` chat is still shown. The ✕ icon is white |
| 6 | Click `Discard` and confirm | The Instructions go back to the saved text |

---

## Expected Final State

Skill A is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- Test opens as a column with no run started.
- Full screen hides the other columns and restores them.
- Edits and the test chat survive closing and reopening Test.

**Fail:**
- A run starts on opening, or Test opens elsewhere.
- Full screen does not hide or restore the columns.
- Edits or the test chat are lost.

---

## Notes

- Covers AC7 of EliteaAI/elitea_issues#7573.
- The Test column is resizable and starts at about a third of the window (it shares its saved width with Agents), so the three columns are not exactly equal in width.
- Steps verified on DEV against EliteaUI#1575 on 2026-11-25.
