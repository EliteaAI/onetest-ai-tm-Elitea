---
id: ELITEA-2584
title: "Trace steps endpoint supports pagination with limit and offset"
priority: high
type: functional
module: trace-steps-api
status: ready
execution_type: manual
tags: [nfr:performance, eng:backend, epic:5724]
requirements: [EliteaAI/elitea_issues#5724, EliteaAI/elitea_issues#5727]
---
# ELITEA-2584: Trace steps endpoint supports pagination with limit and offset

**Module:** Trace Steps API · **Priority:** High · **Type:** Functional

**Objective:** Verify that the new trace steps endpoint supports pagination via `limit` and `offset` parameters for efficient data loading.

**Coverage:**
- Endpoint accepts limit parameter
- Endpoint accepts offset parameter
- Pagination returns correct subset of data
- Multiple pages can be fetched sequentially

## Preconditions

- Logged in to {{base_url}}
- Access to a conversation with multiple tool calls (>5)
- API testing tool available (Postman, curl, or DevTools)

## Test Data

| Field | Value |
|-------|-------|
| Conversation | One with 10+ tool calls in a single turn |
| Limit | 3 |
| Offset | 0, 3, 6 |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create/find a conversation with 10+ tool calls | Conversation with multiple tool calls exists |
| 2 | Call trace steps endpoint with limit=3, offset=0 | Returns first 3 trace steps |
| 3 | Call trace steps endpoint with limit=3, offset=3 | Returns next 3 trace steps (different from step 2) |
| 4 | Call trace steps endpoint with limit=3, offset=6 | Returns next 3 trace steps (different from steps 2 and 3) |
| 5 | Verify no duplicates across pages | All returned steps are unique |
| 6 | Call with offset beyond total count | Returns empty array, no error |
| 7 | Call with limit=0 | Returns empty array or error (document behavior) |

## Expected Final State

Pagination works correctly — different offset values return different subsets of data with no duplicates or missing items.

## Pass/Fail Criteria

**Pass:**
- limit and offset parameters work as expected
- No duplicates across paginated results
- Edge cases (offset > total, limit=0) handled gracefully

**Fail:**
- Pagination returns wrong data
- Duplicates appear across pages
- Server error on edge cases
