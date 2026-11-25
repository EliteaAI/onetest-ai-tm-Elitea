---
id: ELITEA-4893
title: "Skill page: Settings layout, Instructions preview/code with Copy, and Test column with Full screen"
priority: critical
type: regression
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.9, automated:UI:regression]
requirements: [EliteaAI/elitea_issues#7573]
---

# ELITEA-4893: Skill page: Settings layout, Instructions preview/code with Copy, and Test column with Full screen

**Module:** skills · **Priority:** critical · **Type:** regression

**Objective:** Verify the main skill page journey in the split layout: the page opens on Settings with the Instructions on the right, preview and code switch with Copy only in code mode and no full-screen button for the instructions, and Test opens as a column that keeps the unsaved edits and the chat.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Editor or Admin role in the project.
- Skill `regression-skill-layout` exists and is saved, with the Instructions from Test Data and at least one bundled file. If it does not exist, create it, then add a file in **Files → +** (Add files).

---

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all` |
| Skill | `regression-skill-layout` |
| Marker | `LAYOUT-MARKER` |

Instructions body:

~~~markdown
# Layout skill
See references/guide.md for details.
Reply with LAYOUT-OK.
~~~

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the skill | The `Settings` tab is active; the tab bar shows `Files – N` and `Edit with AI`. GENERAL is expanded; RUN SETTINGS and INFORMATION are collapsed. "Instructions (SKILL.md)" is on the right, in preview |
| 2 | Check the Instructions header | `Test`, the eye ("Preview mode") and `</>` ("Edit mode") are shown. There is no Copy and no full-screen button |
| 3 | Click `</>` and add `LAYOUT-MARKER` at the end | The source is shown with line numbers and frontmatter. Copy appears left of `Test`. `Save` and `Discard` become enabled |
| 4 | Click Copy | The toast "The instructions have been copied to the clipboard." appears. The clipboard holds the whole source with `LAYOUT-MARKER` |
| 5 | Click the eye, then `</>` | `LAYOUT-MARKER` is shown in both modes. Copy is hidden in preview |
| 6 | Click `Test` | A `Test` column opens on the right with the "Testing unsaved changes" banner. No message is sent |
| 7 | Send `hello` | The reply contains `LAYOUT-OK` |
| 8 | Click Fullscreen mode, then Exit fullscreen mode | The Settings and Instructions columns hide, then come back. `LAYOUT-MARKER` is still in the editor |
| 9 | Close Test (✕) and open it again, then click `Discard` and confirm | The earlier chat is still shown. After Discard the Instructions go back to the saved text |

---

## Expected Final State

The skill is unchanged.

---

## Pass/Fail Criteria

**Pass:**
- Layout, modes, Copy placement, the Test column and Full screen work; edits and the chat survive.

**Fail:**
- Wrong default tab or collapsed state, Copy in preview, a full-screen button for the instructions.
- A run starts when Test opens, or edits or the chat are lost.

---

## Notes

**Source functional tests:** ELITEA-4885, ELITEA-4886, ELITEA-4887 (AC1–AC4, AC6, AC7 of EliteaAI/elitea_issues#7573)
**Regression rationale:** Core edit-and-test journey on the new skill page layout.
**Selected checkpoints:** default tab and collapsed sections; Copy only in code mode; no full-screen button for the instructions; Test column without auto-run; Full screen; edits and chat survive.
**Not duplicated here:** the Edit with AI flow (ELITEA-2611), Save As Version (ELITEA-4747), the Viewer role (ELITEA-4748), the narrow window (ELITEA-4888).
