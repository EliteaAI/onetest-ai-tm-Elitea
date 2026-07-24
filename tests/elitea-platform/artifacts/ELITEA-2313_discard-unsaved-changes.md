---
id: ELITEA-2313
title: "Discard Unsaved Changes"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-2313: Discard Unsaved Changes

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify Discard functionality restores the last saved version

## Preconditions

- MDX file is open in Raw mode
- User has made changes but NOT saved

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open `test_file_1_under_1mb.mdx` in Raw mode | File opens in Raw mode |
| 2 | Make a change: Change line 7 text to "TEST DISCARD CHANGE" | Text is modified |
| 3 | Observe Save and Discard buttons are active | Both buttons enabled |
| 4 | Click "Discard" button | Confirmation dialog appears |
| 5 | Observe confirmation dialog | Dialog shows warning message |
| 6 | Click "Discard" in the confirmation dialog | Dialog closes |
| 7 | Observe the content | Original content restored |

## Expected Results

- After making changes, Discard button becomes active
- Confirmation dialog displays with message: "Are you sure you want to discard changes?"
- Dialog has two buttons: "Cancel" and "Discard"
- Clicking "Discard" closes the dialog
- Content reverts to original (line 7 shows original text)
- Change "TEST DISCARD CHANGE" is removed
- Save button becomes inactive (gray/disabled)

## Pass/Fail Criteria

**Pass:**
- Discard button activates after changes
- Confirmation dialog appears
- Content reverts to last saved state
- Save button deactivates after discard

**Fail:**
- Discard button doesn't activate
- No confirmation dialog
- Content doesn't revert
- Changes remain after discard
