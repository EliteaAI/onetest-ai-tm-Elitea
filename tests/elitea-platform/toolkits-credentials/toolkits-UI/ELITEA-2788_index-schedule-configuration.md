---
id: ELITEA-2788
title: "Index Schedule Configuration Display and Toggle"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, indexes, schedule]
requirements: []
---
# ELITEA-2788: Index Schedule Configuration Display and Toggle

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify schedule section displays correctly and schedule toggle works.

**Coverage:**
- Schedule section visible on Index Details page
- Empty state shows "Schedule is not configured yet"
- Configured schedule shows time, timezone, next run
- Schedule toggle enables/disables schedule
- Edit and delete actions available

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with an index that has scheduling capability

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with indexing |
| Index | An index with or without configured schedule |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Index Details page for an index without schedule. | Index details page displays. |
| 2 | Observe the SCHEDULE section (collapsed by default). | Section header "SCHEDULE" visible with collapse/expand toggle. |
| 3 | Expand the SCHEDULE section. | Section expands; shows "Schedule is not configured yet" message if no schedule. |
| 4 | For an index with configured schedule, observe the schedule card. | Card shows: time (e.g., "At 00:00, only on Saturday"), timezone info (e.g., "Scheduled: Europe/Minsk, Shown: Asia/Yerevan"), Next run date. |
| 5 | Verify the toggle switch on the schedule card. | Toggle switch visible; can be turned on/off. |
| 6 | Toggle the schedule off. | Schedule is disabled; next run may update or show as disabled. |
| 7 | Toggle the schedule back on. | Schedule is re-enabled. |
| 8 | Verify edit (pencil) and delete (trash) icons are present. | Action icons visible on schedule card. |

## Expected Final State

Schedule section displays correct configuration with functional toggle and action buttons.

## Pass/Fail Criteria

**Pass:**
- Schedule section visible and expandable
- Empty state message when no schedule
- Configured schedule shows all details
- Toggle enables/disables schedule
- Edit and delete icons present

**Fail:**
- Schedule section missing
- Incorrect schedule information
- Toggle doesn't work
- Missing action icons
