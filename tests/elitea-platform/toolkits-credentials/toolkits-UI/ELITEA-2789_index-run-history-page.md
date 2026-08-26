---
id: ELITEA-2789
title: "Index Run History Page Display and Navigation"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, indexes, history]
requirements: []
---
# ELITEA-2789: Index Run History Page Display and Navigation

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify Run History page displays indexing events correctly.

**Coverage:**
- Run History button navigates to history page
- History table shows Date, Event, Duration columns
- History entries show correct event labels
- Share link option available
- Right panel shows JSON configuration for selected entry

## Preconditions

- Logged in to {{base_url}}
- An index with at least one completed indexing operation (has history)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with indexes |
| Index | An index with multiple history entries |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Index Details page. | Index details page displays. |
| 2 | Click the "Run History" button in the header. | History page opens. |
| 3 | Verify breadcrumb. | Shows: "Toolkits & Indexes / [Toolkit] / [Index] / History". |
| 4 | Observe the history table columns. | Table shows: Date, Event, Duration columns. |
| 5 | Verify history entries content. | Entries show date/time, event type ("Reindexed" or "Reindexed by [user]"), duration (e.g., "1.59 s"). |
| 6 | Click the 3-dot menu on a history entry. | Context menu appears with "Share link" option. |
| 7 | Click "Share link". | Link copied to clipboard or share dialog appears. |
| 8 | Observe the right panel. | Shows JSON configuration details for the selected/hovered entry. |
| 9 | Scroll through multiple history entries. | Entries are scrollable; table handles many entries. |

## Expected Final State

Run History page displays all indexing events with correct metadata, share functionality, and configuration details.

## Pass/Fail Criteria

**Pass:**
- Run History button navigates correctly
- Table shows all required columns
- Event labels are accurate
- Share link option works
- Right panel shows configuration

**Fail:**
- Navigation fails
- Missing columns or data
- Incorrect event labels
- Share link missing
- Configuration panel empty
