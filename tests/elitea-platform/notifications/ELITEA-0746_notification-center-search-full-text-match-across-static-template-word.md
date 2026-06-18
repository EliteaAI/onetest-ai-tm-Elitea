---
id: ELITEA-0746
title: "Notification Center Search — Full-Text Match Across Static Template Words, Entity Tokens, and Mixed Phrases"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4696]
---
# ELITEA-0746: Notification Center Search — Full-Text Match Across Static Template Words, Entity Tokens, and Mixed Phrases

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the Notification Center search field performs full-text matching against the complete rendered notification text — including static template words (e.g. "is successfully", "will start deleting") as well as dynamic entity tokens (entity type, name, and numeric payload) — and returns correct result counts for every query variant.

**Coverage:**
- Static template-word-only queries return all matching notifications instead of zero results (core bug fix)
- Mixed queries combining entity name with template words return correct results
- "No notifications" is never shown when matching notifications actually exist
- Entity type label searches continue to work (regression)
- Numeric payload searches continue to work (regression)
- Entity name searches continue to return results (regression; partial issue with `test 2` noted separately)
- Clearing the search field restores all notifications
- Edge case: single-word static keyword query ("successfully") matches multiple notification types

## Preconditions

- User is logged in to {{base_url}}
- The following notifications are present in the Notification Center (create the underlying entities and trigger the notifications as needed before running this test case):
  - `Index test 2 is successfully created: { "indexed": 759 }` — appears **twice** (two separate indexing runs)
  - `Index test 1 is successfully created: { "indexed": 43 }`
  - `Index test 3 is successfully created: { "indexed": 0 }`
  - `Bucket retention1weeks will start deleting files in 24 hours...`
  - `Project was successfully created.`
- Total pre-existing notifications: at least 6 (5 unique texts, 1 duplicate)
- Notification Center is accessible via the bell icon / left-sidebar notification link
- Browser: any modern Chromium-based browser

## Test Data

Notification texts present before search:
| # | Full Notification Text | Count |
|---|---|---|
| 1 | `Index test 2 is successfully created: { "indexed": 759 }` | ×2 |
| 2 | `Index test 1 is successfully created: { "indexed": 43 }` | ×1 |
| 3 | `Index test 3 is successfully created: { "indexed": 0 }` | ×1 |
| 4 | `Bucket retention1weeks will start deleting files in 24 hours...` | ×1 |
| 5 | `Project was successfully created.` | ×1 |

Search queries and expected result counts (post-fix):
| Query | Expected count | Matching notifications |
|---|---|---|
| `is successfully` | 5 | All four Index notifications + Project notification |
| `2 is successfully` | 2 | Both "Index test 2" entries |
| `was successfully` | 1 | "Project was successfully created." |
| `will start deleting` | 1 | Bucket retention1weeks notification |
| `successfully` | 6 | All notifications containing the word |
| `Index` | 5 | All four Index notifications (×2 for test 2 = 5 total) |
| `test 2` | 2 | Both "Index test 2" entries |
| `759` | 2 | Both "Index test 2" entries |
| (empty / cleared) | 6 | All notifications restored |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Notification Center. | Notification Center is displayed. All pre-existing notifications are visible. |
| 2 | In the Search field, type: `is successfully` | Search results update. One or more notifications are displayed. The 'No notifications' empty state is NOT shown. |
| 3 | Clear the search field. | All notifications are restored in the list. |
| 4 | Type in the Search field: `2 is successfully` | One or more notifications are displayed. The 'No notifications' empty state is NOT shown. |
| 5 | Clear the search field. | All notifications are restored in the list. |
| 6 | Type in the Search field: `was successfully` | One or more notifications are displayed. The 'No notifications' empty state is NOT shown. |
| 7 | Clear the search field. | All notifications are restored in the list. |
| 8 | Type in the Search field: `will start deleting` | One or more notifications are displayed. The 'No notifications' empty state is NOT shown. |
| 9 | Clear the search field. | All notifications are restored in the list. |
| 10 | Type in the Search field: `successfully` (single keyword present in multiple notification types) | One or more notifications are displayed. The 'No notifications' empty state is NOT shown. |
| 11 | Clear the search field. | All notifications are restored in the list. |
| 12 | Type in the Search field: `Index` (entity type label) | One or more notifications are displayed. (Regression: this query worked before the fix.) |
| 13 | Clear the search field. | All notifications are restored in the list. |
| 14 | Type in the Search field: `test 2` (entity name token) | One or more notifications are displayed. (Regression: verify results are returned.) |
| 15 | Clear the search field. | All notifications are restored in the list. |
| 16 | Type in the Search field: `759` (numeric payload token) | One or more notifications are displayed. (Regression: this query worked before the fix.) |
| 17 | Clear the search field completely (backspace all characters or click X icon). | All notifications are restored immediately. The Notification Center returns to its default unfiltered state. |

## Expected Final State

All notifications are restored immediately. The Notification Center returns to its default unfiltered state.

## Pass/Fail Criteria

**Pass:**
- Steps 2, 4, 6, 8: Static template-word queries (`is successfully`, `2 is successfully`, `was successfully`, `will start deleting`) each return one or more results and never show the "No notifications" empty state
- Step 10: Single-keyword cross-type query (`successfully`) returns one or more notifications
- Steps 12, 14, 16: Regression queries (`Index`, `test 2`, `759`) return one or more results with no regression from pre-fix behavior
- Step 17: Clearing the search restores all notifications
- No unexpected errors, crashes, or loading spinners that do not resolve

**Fail:**
- Any of Steps 2, 4, 6, or 8 shows "No notifications" instead of results
- Step 10 returns no results for the query `successfully`
- Steps 12, 14, or 16 return no results (regression)
- Clearing the search field (Step 17) does not restore all notifications
- The Notification Center is unresponsive or crashes after any search query
