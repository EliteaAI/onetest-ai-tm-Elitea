---
id: ELITEA-1861
title: "File Preview/Edit – Switching Between Preview and Raw Tabs"
priority: medium
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:artifacts]
requirements: []
---

# ELITEA-1861: File Preview/Edit – Switching Between Preview and Raw Tabs

**Module:** artifacts · **Priority:** medium · **Type:** functional

**Objective:** Verify that switching between the Preview and Raw tabs for a Markdown file correctly toggles button states and content rendering, without losing the original file content.

---

## Preconditions

- User is logged in to the Elitea platform.
- Bucket "bucket-1" contains "project-background.md".

---

## Test Data

| Field | Value |
|-------|-------|
| Bucket name | bucket-1 |
| File name | project-background.md |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Artifacts section and open "project-background.md" via the "View/Edit file" icon | Editor opens |
| 2 | Verify "Preview" tab is active by default — Save and Discard are inactive | Preview tab is active; buttons are inactive |
| 3 | Click "Raw" tab — verify Raw content is shown with line numbers, Save and Discard become active | Raw tab is active; raw content with line numbers shown; buttons become active |
| 4 | Click "Preview" tab again — verify formatted Markdown is shown, Save and Discard become inactive again | Preview tab active; rendered Markdown shown; buttons inactive |
| 5 | Verify switching tabs does not lose the original file content | Original content is intact after switching |

---

## Expected Final State

Tabs switch correctly between Preview (inactive buttons, rendered view) and Raw (active buttons, editable view). Original content is preserved throughout tab switching.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Button states toggle correctly with tabs; original content preserved.

**Fail:**
- Any step produces an error or unexpected result.
- Button states do not change with tabs, or content is lost during switching.
