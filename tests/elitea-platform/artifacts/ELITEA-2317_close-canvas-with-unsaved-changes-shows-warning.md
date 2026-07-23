---
id: ELITEA-2317
title: "Close Canvas with Unsaved Changes Shows Warning"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-2317: Close Canvas with Unsaved Changes Shows Warning

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify closing Canvas with unsaved changes displays warning dialog with save options

## Preconditions

- MDX file is open in Canvas
- Changes have been made but not saved

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open MDX file in Raw mode | File opens |
| 2 | Make changes to the content | Content modified |
| 3 | Click Close button (X) in Canvas header | Action initiated |
| 4 | Observe warning dialog appears | Dialog displays |
| 5 | Note dialog options: Save, Discard, Cancel | Three options visible |
| 6 | Click "Cancel" button | Dialog closes, Canvas remains open |
| 7 | Click Close (X) again | Dialog reappears |
| 8 | Click "Discard" button | Canvas closes, changes lost |

## Expected Results

- Closing without unsaved changes closes Canvas immediately
- Closing with unsaved changes shows warning dialog
- Warning dialog displays message about unsaved changes
- Dialog offers three options: "Save", "Discard", "Cancel"
- "Cancel" keeps Canvas open with changes preserved
- "Discard" closes Canvas without saving
- "Save" saves changes and then closes Canvas
- After any action, Canvas behaves as expected

## Pass/Fail Criteria

**Pass:**
- Warning dialog appears with unsaved changes
- All three buttons work correctly
- Unsaved changes preserved when cancelled
- Canvas closes appropriately after Save/Discard

**Fail:**
- No warning dialog appears
- Changes lost without warning
- Dialog buttons don't work
- Canvas behavior is incorrect
