---
id: ELITEA-2800
title: "Regression - Run History and Schedule Display"
priority: high
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, toolkit-redesign, history, schedule]
requirements: []
---
# ELITEA-2800: Regression - Run History and Schedule Display

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Regression

**Objective:** Verify Run History page and Schedule section display correctly in the redesigned UI.

**Coverage:**
- Run History button navigation
- History table with Date, Event, Duration
- Share link functionality
- Schedule section display
- Schedule toggle functionality

## Preconditions

- Logged in to {{base_url}}
- An index with run history and optionally a configured schedule

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with indexes |
| Index | Index with history entries |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Index Details page. | Page opens with Run History button visible. |
| 2 | Click "Run History" button. | History page opens. |
| 3 | Verify breadcrumb shows full path including "History". | Breadcrumb correct. |
| 4 | Verify history table columns: Date, Event, Duration. | All columns visible. |
| 5 | Verify entries show correct data format. | Date/time, "Reindexed" event, duration in seconds. |
| 6 | Click 3-dot menu on an entry → Share link. | Link copied or share dialog appears. |
| 7 | Navigate back to Index Details. | Page displays. |
| 8 | Expand SCHEDULE section. | Section expands. |
| 9 | If schedule exists, verify display (time, timezone, next run, toggle). | All schedule info visible. |
| 10 | Toggle schedule on/off. | Schedule state changes. |

## Expected Final State

Run History and Schedule sections display and function correctly.

## Pass/Fail Criteria

**Pass:**
- Run History navigates and displays correctly
- History entries show accurate data
- Share link works
- Schedule section displays and toggle works

**Fail:**
- Navigation fails
- Missing or incorrect history data
- Share link broken
- Schedule display or toggle fails
