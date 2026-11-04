---
id: ELITEA-4335
title: "Verify Status filter returns accurate results in Run History"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6927]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Skill has run history with multiple statuses (success, error, stopped)
- At least 3 runs exist for each status type

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all/[skillId]/history` |
| Status Types | Success, Error, Stopped, All |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skill Run History page | Run History table displays all runs |
| 2 | Locate the status filter control | Status filter dropdown is visible |
| 3 | Select "Success" status filter | Table updates to show only successful runs |
| 4 | Verify all displayed runs have success status | All runs show success icon/indicator |
| 5 | Change filter to "Error" status | Table updates to show only failed runs |
| 6 | Verify all displayed runs have error status | All runs show error icon/indicator |
| 7 | Change filter to "Stopped" status | Table updates to show only stopped runs |
| 8 | Verify all displayed runs have stopped status | All runs show stopped icon/indicator |
| 9 | Select "All" or clear the filter | Table returns to showing all runs regardless of status |

## Expected Final State

Status filter accurately filters run history by execution status, showing only runs matching the selected status.

## Pass/Fail Criteria

**Pass:**
- Status filter control is accessible
- Filtering by each status type (Success, Error, Stopped) works correctly
- All displayed runs match the selected status
- Status indicators (icons) match the filter
- Clearing the filter restores all runs

**Fail:**
- Status filter is missing or non-functional
- Runs with incorrect status are displayed
- Filtering does not update the table
- Status indicators do not match the filter criteria
