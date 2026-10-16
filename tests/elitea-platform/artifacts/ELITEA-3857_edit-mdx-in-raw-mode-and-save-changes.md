---
id: ELITEA-3857
title: "Edit MDX in Raw Mode and Save Changes"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, feat:canvas, r-2.0.5]
requirements: [EliteaAI/elitea_issues#5846]
---
# ELITEA-3857: Edit MDX in Raw Mode and Save Changes

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify user can edit MDX source in Raw mode and successfully save changes

## Preconditions

- MDX file is open in Raw mode
- User has write permission to Artifacts

## Test Data

- Original heading: `## Introduction!!!`
- Modified heading: `## Introduction - EDITED`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Raw mode, locate line 5: `## Introduction!!!` | Line is visible in editor |
| 2 | Change the text to: `## Introduction - EDITED` | Text is editable |
| 3 | Observe Save button state | Save button becomes active (teal) |
| 4 | Click "Save" button (top-right) | Save operation initiates |
| 5 | Wait for save to complete | Save completes successfully |
| 6 | Click on "Preview" tab | Mode switches to Preview |
| 7 | Verify the change appears in rendered content | Updated heading displays |

## Expected Results

- Text editing is allowed in Raw mode
- Cursor appears and characters can be typed
- After modification, Save button becomes active/enabled (teal color)
- Clicking Save shows progress indicator (if any)
- Save completes without errors
- Success message or confirmation appears
- Save button becomes inactive again after save
- Switching to Preview shows updated heading: "Introduction - EDITED"
- File timestamp updates in Artifacts listing

## Pass/Fail Criteria

**Pass:**
- Edit operations work smoothly
- Save button activates after changes
- Changes persist after save
- Preview reflects saved changes

**Fail:**
- Cannot edit text in Raw mode
- Save button doesn't activate
- Save operation fails
- Changes not reflected in Preview
