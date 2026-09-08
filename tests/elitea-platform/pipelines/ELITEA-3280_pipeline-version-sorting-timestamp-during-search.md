---
id: ELITEA-3280
title: "Pipeline version sorting by timestamp maintained during search"
priority: high
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:pipelines, feat:version-selector, feat:search, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor/Admin role
- Private project context is selected
- Pipeline exists with multiple versions having known creation timestamps

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/pipelines` |
| Pipeline | Pipeline with versions created at different times |
| Version "v1" | Created Jan 1, 2026, 10:00 AM |
| Version "v2" | Created Jan 15, 2026, 03:30 PM |
| Version "v3" | Created Jan 10, 2026, 11:00 AM |
| Expected order | v2 (newest), v3, v1 (oldest) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipeline with versions created at different times | Pipeline loads |
| 2 | Open the version selector dropdown | Dropdown displays all versions |
| 3 | Verify versions are sorted by creation timestamp (newest first) | Order is: v2, v3, v1 |
| 4 | Note the timestamps displayed for each version | Timestamps confirm newest-first order |
| 5 | Type a search query that matches multiple versions (e.g., "v") | Search filters to matching versions |
| 6 | Verify the filtered results maintain newest-first sort order | Filtered list is still sorted by timestamp (newest first) |
| 7 | Clear the search field | Full list returns |
| 8 | Verify sort order remains consistent after clearing search | Order is still: v2, v3, v1 |
| 9 | Perform another search with different query | Multiple matches return |
| 10 | Verify sort order is maintained again | Newest-first order is preserved |

## Expected Final State

Pipeline versions remain sorted by creation timestamp (newest first) both in the full list and in filtered search results. Sort order is consistent and stable.

## Pass/Fail Criteria

**Pass:**
- Versions are sorted newest-first by creation timestamp in full list
- Filtered search results maintain newest-first sort order
- Sort order is consistent before, during, and after search
- Timestamps displayed confirm correct ordering

**Fail:**
- Versions are not sorted by creation timestamp
- Search results break the sort order
- Sort order is inconsistent or random
- Timestamps do not match the displayed order
