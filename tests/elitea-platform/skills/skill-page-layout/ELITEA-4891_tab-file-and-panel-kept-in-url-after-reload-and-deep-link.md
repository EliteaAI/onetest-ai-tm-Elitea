---
id: ELITEA-4891
title: "Tab, open file and side panel are kept in the URL and restored after a reload or deep link"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7573]
---

# ELITEA-4891: Tab, open file and side panel are kept in the URL and restored after a reload or deep link

**Module:** skills · **Priority:** high · **Type:** functional

**Objective:** Verify that the tab, the open file and the side panel are kept in the URL (`view`, `file`, `panel`) and the same state opens after a reload or from a shared link.

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
| 1 | Open Skill A → `Files – 4` → `guide.md` → `Instructions`. Make no edits | The URL has `view=files`, `file=references%2Fguide.md` and `panel=instructions` |
| 2 | Reload the page | The same tab, file and panel open |
| 3 | In a new tab, open the skill URL with `&view=files&file=scripts%2Frun.py&panel=test` | `run.py` and Test open beside the tree. No run starts |
| 4 | Open the skill URL with `&view=files&file=nope%2Fmissing.md` | "nope/missing.md is not in this version." is shown. The page does not crash |
| 5 | Open the skill URL with no extra parameters | The page opens on `Settings` with no side panel |

---

## Expected Final State

Skill A is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- The state is written to the URL and restored on reload and from a deep link.
- A missing file is reported without a crash.

**Fail:**
- The URL is not updated, or the state is lost after reload.
- A deep link opens another state or starts a run.

---

## Notes

- Covers AC12 of EliteaAI/elitea_issues#7573. The order of the parameters in the URL can vary.
- Steps verified on DEV against EliteaUI#1575 on 2026-11-25.
