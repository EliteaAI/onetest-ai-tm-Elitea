---
id: ELITEA-2707
title: "Discard unsaved changes"
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
| 1 | Open HTML file in Raw mode | Raw mode displays HTML source code |
| 2 | Make changes to HTML source (e.g., change a heading text) | Changes are made in the editor |
| 3 | Observe Save and Discard buttons | Both buttons become active |
| 4 | Click "Discard" button | Warning dialog appears |
| 5 | Observe the warning dialog content | Dialog shows title, message, and buttons |
| 6 | Click "Cancel" button | Dialog closes, changes remain intact |
| 7 | Click "Discard" button again | Warning dialog appears again |
| 8 | Click "Confirm" button | Changes are discarded |

## Expected Final State

- Original content is restored in the editor
- Save button becomes inactive after confirming discard
- No unsaved changes remain

## Pass/Fail Criteria

**Pass:**
- Discard button is active when changes are made
- Warning dialog displays with title "Warning"
- Dialog message: "You are editing now. Do you want to discard current changes and continue?"
- Dialog has "Cancel" and "Confirm" (red) buttons
- Cancel keeps changes intact
- Confirm restores original content

**Fail:**
- Discard button is not active after making changes
- No warning dialog appears
- Dialog text is incorrect
- Cancel discards changes
- Confirm does not restore original content
