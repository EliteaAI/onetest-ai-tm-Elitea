---
id: ELITEA-3318
title: "Version comparison modal opens with side-by-side layout displaying Agent version columns"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Agent exists with 2+ versions (e.g., "base", "v1.0")

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Test Agent | Agent with versions: "base", "v1.0" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to the Test Agent details page | Agent page loads successfully |
| 2 | Click the "Compare Versions" button in the actions menu | Modal opens without errors |
| 3 | Verify modal displays two version columns side-by-side | Two columns are visible with equal width |
| 4 | Verify left column header shows actual version name (e.g., "base") | Left column labeled with correct version name |
| 5 | Verify right column header shows actual version name (e.g., "v1.0") | Right column labeled with correct version name |
| 6 | Verify modal has X close button in top-right corner | Close button is visible |
| 7 | Click X button | Modal closes and returns to Agent details page |
| 8 | Reopen modal and verify Cancel/Close action button exists | Cancel button is visible at bottom |
| 9 | Click Cancel | Modal closes successfully |

## Expected Final State

Version comparison modal opens displaying two Agent versions side-by-side with correct version names in column headers and functional close controls.

## Pass/Fail Criteria

**Pass:**
- Modal opens successfully on button click
- Two version columns displayed side-by-side
- Column headers show actual version names (not generic labels)
- Modal can be closed via X button or Cancel action

**Fail:**
- Modal fails to open or displays errors
- Columns not displayed side-by-side
- Generic labels used instead of version names ("Version A", "Version B")
- Cannot close modal
