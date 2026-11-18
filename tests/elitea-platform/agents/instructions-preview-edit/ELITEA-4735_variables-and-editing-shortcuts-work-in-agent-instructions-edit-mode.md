---
id: ELITEA-4735
title: "Variables, autosuggest, and editing shortcuts work in agent Instructions Edit mode"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7377]
---

# ELITEA-4735: Variables, autosuggest, and editing shortcuts work in agent Instructions Edit mode

**Module:** agents · **Priority:** high · **Type:** functional

**Objective:** Verify that the Markdown-highlighted agent Instructions editor keeps the existing editing features: `/` autosuggest, variable detection, undo/redo, large paste and line endings.

---

## Preconditions

- User is logged in to `{{base_url}}` with the Admin or Editor role.
- "QA-7377 Agent" has at least one configured toolkit or participant, so that autosuggest has items to show.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent | QA-7377 Agent |
| Variable | `{{new_var}}` |
| Large paste | 1,000+ lines of text |
| Line-ending sample | Multi-line text with Windows (CRLF) line endings, copied from an external editor |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Switch INSTRUCTIONS to Edit and type `/` | The autosuggest dropdown with toolkits, MCPs, agents and pipelines appears |
| 2 | Select an item | The mention is inserted in the editor |
| 3 | Type `{{new_var}}` | The VARIABLES section detects `new_var` as before |
| 4 | Switch to Preview | The variable text is shown, and the rest of the content renders normally |
| 5 | Switch to Edit. Press Ctrl+Z several times, then Ctrl+Y | Undo removes the recent edits step by step, and Redo restores them |
| 6 | Press Ctrl+A, cut, then paste back | The whole content is selected, cut and restored without changes |
| 7 | Paste the 1,000+ line text | The paste finishes without freezing. All lines are present |
| 8 | Press Tab and Shift+Tab inside a list line | Indentation changes as expected, and focus does not leave the editor |
| 9 | Paste the CRLF line-ending sample, then Discard all changes | The pasted text is not reformatted (no extra blank lines). Discard restores the saved content |

---

## Expected Final State

"QA-7377 Agent" is unchanged after Discard.

---

## Pass/Fail Criteria

**Pass:**
- Autosuggest, variable detection, undo/redo, select-all, large paste, Tab handling and line endings behave as before.

**Fail:**
- Any of these features is missing or broken, or content is reformatted in the new editor.

---

## Notes

- Re-run ELITEA-0089 (autosuggest triggers on `/` in the Instructions editor only) and the related autosuggest cases ELITEA-0070 to ELITEA-0088.
