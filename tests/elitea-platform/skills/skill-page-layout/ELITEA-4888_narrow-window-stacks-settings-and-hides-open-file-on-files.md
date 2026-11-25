---
id: ELITEA-4888
title: "Below 1200 px the instructions stack under the settings, and the open file hides on Files"
priority: medium
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7573]
---

# ELITEA-4888: Below 1200 px the instructions stack under the settings, and the open file hides on Files

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify the narrow-window layout (below 1200 px): on Settings with Test open, the instructions go under the settings and the left column scrolls as one; on Files with Instructions or Test open, the open file hides while the tree and the panel stay.

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
| 1 | Set the window width to 1100 px. Open Skill A, click `Test`, and expand RUN SETTINGS and INFORMATION | The left column holds GENERAL, RUN SETTINGS, INFORMATION and, below them, the Instructions. Test is on the right |
| 2 | Scroll the left column | All sections and the instructions are shown whole. The whole left column scrolls as one, with no separate scroll inside the settings or the instructions |
| 3 | Open `Files – 4` and click `references/guide.md` | The open file is hidden. The tree and Test stay |
| 4 | Close Test, then click `Instructions` in the file header | The open file stays hidden. The tree and the Instructions panel stay |
| 5 | Set the window width back to 1366 px | The open file is shown beside the tree and the Instructions. No state is lost |

---

## Expected Final State

Skill A is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- Settings + Test stack and scroll as one column below 1200 px.
- Files with a side panel hides the open file below 1200 px.

**Fail:**
- Separate scrolls inside settings or instructions, or sections cut off.
- The open file stays visible, or the tree or the panel disappears.

---

## Notes

- Covers AC8, AC9 of EliteaAI/elitea_issues#7573.
- Steps verified on DEV against EliteaUI#1575 on 2026-11-25.
