---
id: ELITEA-3295
title: "Version sorting by timestamp maintained during search in Skills"
priority: high
type: functional
module: default-modules
status: ready
execution_type: manual
tags: [feat:skills, feat:version-selector, feat:search, eng:frontend, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6302]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has Editor or Admin role
- Skill with multiple versions exists with known creation timestamps

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Version data | v1 (created Jan 1, 2026), v2 (created Jan 15, 2026), v3 (created Jan 10, 2026) |
| Expected order | v2 (newest), v3, v1 (oldest) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skill with versions created at different times | Skill loads |
| 2 | Open version selector dropdown | Dropdown opens |
| 3 | Verify versions are sorted newest to oldest by creation timestamp | v2 appears first, then v3, then v1 |
| 4 | Type a search query that matches multiple versions (e.g., "v") | Filtered results displayed |
| 5 | Verify filtered results maintain newest-first sort order | Results still sorted by creation timestamp descending |
| 6 | Clear search input | Full list restored |
| 7 | Verify sort order remains consistent | Newest-first order preserved |
| 8 | Perform another search with different query | Filtered results shown |
| 9 | Verify sort order is still newest-first | Sort order maintained |

## Expected Final State

Versions remain sorted by creation timestamp (newest first) even when search filtering is applied. Sort order is consistent before, during, and after search operations.

## Pass/Fail Criteria

**Pass:**
- Initial version list sorted newest to oldest
- Filtered search results maintain newest-first order
- Sort order consistent across all search operations
- Clearing search preserves sort order

**Fail:**
- Versions not sorted by timestamp
- Search results appear in wrong order
- Sort order changes during search
- Inconsistent sorting after clearing search
