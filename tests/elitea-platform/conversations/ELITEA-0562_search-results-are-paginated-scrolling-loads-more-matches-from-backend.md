---
id: ELITEA-0562
title: "Search Results Are Paginated — Scrolling Loads More Matches from Backend"
priority: high
type: functional
module: conversations
status: draft
execution_type: manual
tags: [eng:frontend, eng:backend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4835]
---
# ELITEA-0562: Search Results Are Paginated — Scrolling Loads More Matches from Backend

**Module:** Conversations · **Priority:** High · **Type:** Functional

**Objective:** Verify that when search returns more results than the batch size, scrolling within the search results triggers follow-up backend requests with the same query and incremented offset.

**Coverage:**
- Initial search request uses limit=batch_size and offset=0
- Scrolling to bottom of search results triggers a follow-up GET with same query and incremented offset
- Additional matching conversations are appended (not replaced) in results

## Preconditions

- Logged in to {{base_url}} in the Private project
- User has more conversations than one batch size that match a broad search term
- Browser DevTools → Network tab open and recording

## Test Data

Search term: a single common letter or short word that matches many conversations (e.g., 'a' or 'test')

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Chat page, activate search, and type the broad search term | Initial backend GET fires with query=<term>, limit=<batch_size>, offset=0 |
| 2 | Note the number of conversations shown in the initial search results | Only the first batch of matching results is displayed |
| 3 | Scroll to the bottom of the search results list | A follow-up GET fires with the same query=<term> and an incremented offset value |
| 4 | Observe the sidebar after the second request | Additional matching conversations are appended to the results (not replacing existing ones) |

## Expected Final State

Additional matching conversations are appended to the results (not replacing existing ones)

## Pass/Fail Criteria

**Pass:**
- Scrolling in search results triggers a follow-up request with same query and higher offset
- New results are appended, not replaced

**Fail:**
- All results load at once in a single request with a very high limit
- Scrolling does not trigger any additional network requests
- Results are replaced instead of appended
