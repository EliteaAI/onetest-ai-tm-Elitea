---
id: ELITEA-0376
title: "DOCX Editor - Discard Changes, Unsaved-Changes Guard, and Save/Discard Button States"
priority: critical
type: functional
module: canvas
status: draft
execution_type: manual
tags: [feat:canvas, story:3648]
requirements: [ProjectAlita/projectalita.github.io#3648]
---
# ELITEA-0376: DOCX Editor - Discard Changes, Unsaved-Changes Guard, and Save/Discard Button States

**Module:** Canvas · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Discard workflow, X-close guard dialog, and Save/Discard button enable/disable states in SuperDoc Canvas.

**Coverage:**
- Save and Discard buttons are disabled when no changes exist
- Save and Discard buttons become enabled after an edit
- Discard reverts unsaved changes
- X icon with unsaved changes shows a confirmation dialog
- X icon with no unsaved changes closes without a dialog

## Preconditions

- Logged in to {{base_url}}
- DOCX file `test.docx` open in Canvas SuperDoc editor with no edits made

## Test Data

- File: `test.docx` in bucket `test-docx-bucket`
- Edit text: `"DISCARD_TEST"`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open `test.docx` in Canvas without making any changes | Save and Discard buttons are disabled (grayed out) |
| 2 | Type `DISCARD_TEST` into a paragraph | Save and Discard buttons become enabled |
| 3 | Click the Discard button | Unsaved changes are reverted; `DISCARD_TEST` is removed; Save and Discard buttons become disabled again |
| 4 | Type `DISCARD_TEST` again, then click the X (close) icon | A confirmation dialog appears asking whether to save or discard before closing |
| 5 | Click Discard / Don't Save in the confirmation dialog | Modal closes without saving |
| 6 | Reopen `test.docx` from Artifacts | Document shows the original unmodified content — `DISCARD_TEST` is not present |

## Expected Final State

Document shows the original unmodified content — `DISCARD_TEST` is not present

## Pass/Fail Criteria

**Pass:**
- Buttons are disabled with no changes; enabled after an edit
- Discard reverts changes; buttons return to disabled state
- X icon with unsaved changes triggers the confirmation dialog
- Document shows original content after discarding

**Fail:**
- Buttons are always enabled or always disabled regardless of edit state
- Discard does not revert changes
- X icon closes without a dialog when unsaved changes exist
- Document retains discarded content on reopen
