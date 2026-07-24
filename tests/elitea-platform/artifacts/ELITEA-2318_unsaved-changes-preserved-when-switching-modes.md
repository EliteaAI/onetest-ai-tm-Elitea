---
id: ELITEA-2318
title: "Unsaved Changes Preserved When Switching Modes"
priority: high
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-2318: Unsaved Changes Preserved When Switching Modes

**Module:** Artifacts · **Priority:** High · **Type:** Functional

**Objective:** Verify unsaved changes are preserved when switching between Preview and Raw modes

## Preconditions

- MDX file is open in Raw mode

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open MDX file in Raw mode | File opens |
| 2 | Make a change (e.g., modify a heading text) | Change made |
| 3 | Do NOT save | Changes remain unsaved |
| 4 | Switch to Preview mode | Mode switches |
| 5 | Observe the Preview rendering | Preview displays |
| 6 | Switch back to Raw mode | Returns to Raw |

## Expected Results

- Changes are preserved when switching to Preview mode
- Preview shows the modified content (rendered from current edit state)
- Switching back to Raw mode shows the changes are still there
- Save button remains active throughout mode switching
- No data loss occurs during mode switching

## Pass/Fail Criteria

**Pass:**
- Unsaved changes persist across mode switches
- Preview renders unsaved changes
- No data loss occurs

**Fail:**
- Changes lost when switching modes
- Preview doesn't reflect unsaved changes
- Data corruption occurs
