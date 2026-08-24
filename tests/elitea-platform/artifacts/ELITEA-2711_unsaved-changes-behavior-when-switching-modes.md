---
id: ELITEA-2711
title: "Unsaved changes behavior when switching modes"
priority: high
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

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | Any HTML file from Artifacts |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open HTML file in Raw mode | Raw mode displays HTML source |
| 2 | Make a change (e.g., modify a heading text) | Change is made in the editor |
| 3 | Do NOT save the changes | Save button remains active |
| 4 | Click to switch to Preview mode | Warning dialog may appear |
| 5 | If warning appears, click "Confirm" | Mode switches to Preview |
| 6 | Observe the Preview content | Content displays (original or modified) |
| 7 | Switch back to Raw mode | Raw mode displays |
| 8 | Observe the content state | Content state is consistent |

## Expected Final State

- Mode switching behavior is consistent and predictable
- User understands whether changes are preserved or discarded during mode switch

## Pass/Fail Criteria

**Pass:**
- Warning dialog appears if unsaved changes would be discarded
- Mode switching completes without errors
- Behavior is consistent across multiple switches
- User can predict the outcome based on dialog interaction

**Fail:**
- No warning when changes would be lost
- Mode switching fails or causes errors
- Inconsistent behavior between switches
- Data loss without user awareness
