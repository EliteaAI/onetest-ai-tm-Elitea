---
id: ELITEA-4886
title: "Instructions preview/code switch and Copy only in code mode on Settings, with no full-screen button"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7573]
---

# ELITEA-4886: Instructions preview/code switch and Copy only in code mode on Settings, with no full-screen button

**Module:** skills · **Priority:** critical · **Type:** functional

**Objective:** Verify that the Instructions open in preview, `</>` shows the code with line numbers, the eye goes back, unsaved edits survive the switch, Copy appears only in code mode left of Test and copies the whole current source, and there is no full-screen button for the instructions.

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
| 1 | Open Skill A and check the Instructions header | The Instructions are rendered (preview). The header has `Test`, the eye ("Preview mode", active) and `</>` ("Edit mode"). There is no Copy and no full-screen button |
| 2 | Click `</>` | The source is shown with line numbers, frontmatter included. A Copy icon ("Copy to clipboard") appears left of `Test`. The "N characters left" counter is shown. There is no full-screen button |
| 3 | Add `LAYOUT-MARKER` at the end of the body | `Save` and `Discard` become enabled. The counter goes down |
| 4 | Click Copy and paste the clipboard into a text editor | The toast "The instructions have been copied to the clipboard." appears. The pasted text is the whole source, frontmatter and `LAYOUT-MARKER` included |
| 5 | Click the eye, then `</>` | Preview shows `LAYOUT-MARKER`, and Copy is hidden. Code mode shows the same text, and Copy is visible again |
| 6 | Click `Discard` and confirm | The Instructions go back to the saved text |

---

## Expected Final State

Skill A is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- Preview by default; `</>` and the eye switch modes without losing edits.
- Copy appears only in code mode, left of Test, and copies the whole current source.
- No full-screen button for the instructions.

**Fail:**
- Wrong default mode, or edits lost on switch.
- Copy shown in preview, placed elsewhere, or copying the saved text instead of the current one.
- A full-screen button is shown for the instructions.

---

## Notes

- Covers AC3, AC4, AC6 of EliteaAI/elitea_issues#7573. Detailed Preview / Edit coverage: ELITEA-4746.
- Steps verified on DEV against EliteaUI#1575 on 2026-11-25.
