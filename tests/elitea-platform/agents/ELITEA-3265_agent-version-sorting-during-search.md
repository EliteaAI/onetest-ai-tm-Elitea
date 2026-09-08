---
id: ELITEA-3265
title: "Agent — Version Sorting During Search"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, feat:search, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3265: Agent — Version Sorting During Search

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that versions remain sorted by creation timestamp (newest first) even when search filtering is applied.

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with multiple versions having known creation timestamps
- Versions have names that can be partially matched by search

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with versions created at different times |
| Version v1 | Created Jan 01, 2026, 10:00 AM |
| Version v2 | Created Jan 15, 2026, 03:00 PM |
| Version v3 | Created Jan 10, 2026, 11:00 AM |
| Expected Order | v2 (newest), v3, v1 (oldest) |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent with versions v1, v2, v3 | Agent page loads |
| 2 | Open the version selector dropdown | Dropdown opens showing all versions |
| 3 | Verify versions are sorted newest first | Order is: v2 (Jan 15), v3 (Jan 10), v1 (Jan 01) |
| 4 | Type a search query that matches multiple versions (e.g., "v") | Filtered results display (all three versions match) |
| 5 | Verify the filtered results maintain newest-first sort order | Order remains: v2, v3, v1 (newest to oldest by creation timestamp) |
| 6 | Clear the search | All versions reappear |
| 7 | Verify sort order remains consistent after clearing search | Order is still: v2, v3, v1 |

## Expected Final State

Versions maintain newest-first sort order before search, during filtered search, and after clearing search.

## Pass/Fail Criteria

**Pass:** Versions always sorted by creation timestamp (newest first); sort order maintained during and after search filtering

**Fail:** Incorrect sort order before, during, or after search; alphabetical sorting instead of timestamp; sort order changes unexpectedly
