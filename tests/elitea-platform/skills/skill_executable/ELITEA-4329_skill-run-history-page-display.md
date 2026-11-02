---
id: ELITEA-4329
title: "Verify Skill Run History page displays correctly with all required columns and status icons"
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
- At least one skill exists with previous run history (e.g., "uppercase-text-converter")
- Multiple skill runs exist with different statuses (success, error, stopped)

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all/[skillId]/history` |
| Skill Name | uppercase-text-converter |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skills page | Skills list displays |
| 2 | Open a skill with existing run history | Skill detail page displays |
| 3 | Click on "Run History" tab or button | Run History page loads |
| 4 | Observe the table structure | Table displays with columns: Date, Version, Duration |
| 5 | Verify each run entry shows a status icon | Visual status indicators (success/error/stopped icons) are visible for each run |
| 6 | Check date format for all entries | Dates display in consistent format (MM-DD-YYYY, HH:MM AM/PM) |
| 7 | Verify version column shows correct version names | Version names match the skill versions (e.g., "base") |
| 8 | Check duration column formatting | Duration displays in readable format (e.g., "1.65 s", "7.1 s") |

## Expected Final State

Run History page displays a complete table with Date, Version, and Duration columns, along with visual status icons for each run entry.

## Pass/Fail Criteria

**Pass:**
- All three columns (Date, Version, Duration) are visible and populated
- Status icons display correctly for each run
- Data formatting is consistent across all entries
- Table is scrollable if there are many runs

**Fail:**
- Any column is missing or empty
- Status icons do not display
- Data formatting is inconsistent or unreadable
- Table layout is broken or overlapping
