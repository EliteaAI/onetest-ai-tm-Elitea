---
id: ELITEA-2710
title: "Close Canvas with unsaved changes shows warning"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML file is open in Raw mode
- User has made changes but not saved them

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | Any HTML file from Artifacts |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open HTML file in Canvas and switch to Raw mode | Raw mode displays HTML source |
| 2 | Make changes to HTML source (e.g., add a comment `<!-- test -->`) | Changes appear in the editor |
| 3 | Click the "X" (Close) button in Canvas header | Warning dialog appears |
| 4 | Observe the warning dialog | Dialog shows warning message |
| 5 | Click "Cancel" button | Dialog closes, Canvas remains open with changes |
| 6 | Click the "X" button again | Warning dialog appears again |
| 7 | Click "Confirm" button | Canvas closes, changes are discarded |

## Expected Final State

- Canvas is closed after confirming
- Changes are discarded (not saved)
- User returns to the previous view (Artifacts list or chat)

## Pass/Fail Criteria

**Pass:**
- Warning dialog displays before closing with unsaved changes
- Dialog title: "Warning"
- Dialog message: "You are editing now. Do you want to discard current changes and continue?"
- Dialog buttons: "Cancel" and "Confirm" (red button)
- Cancel keeps Canvas open with changes intact
- Confirm closes Canvas and discards changes

**Fail:**
- No warning dialog appears when closing with unsaved changes
- Canvas closes without warning
- Cancel button closes the Canvas
- Changes are saved unexpectedly
