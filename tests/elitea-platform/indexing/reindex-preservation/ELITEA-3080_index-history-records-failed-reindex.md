---
id: ELITEA-3080
title: "Index History Records Failed Reindex with Error Details"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, history]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3080: Index History Records Failed Reindex with Error Details

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that failed reindex operations are recorded in Index History with error details and confirmation that the previous active index was retained.

**Coverage:**
- History entry created for failed reindex
- Event type shows "Reindex failed"
- Error details are included
- Entry confirms previous index retained

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed index
- Ability to cause reindex failure

## Test Data

- Index: Toolkit index with external integration
- Failure method: Token revocation or network block

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab, select an index, open History tab. | History tab displayed. |
| 2 | Note current history entries count. | Count noted. |
| 3 | Cause a reindex failure condition (e.g., revoke token). | Failure condition set. |
| 4 | Initiate Reindex. Wait for failure. | Reindex fails. |
| 5 | Refresh/reopen History tab. | History updated. |
| 6 | Verify new entry was created. | Entry count increased. |
| 7 | Verify entry event type. | Shows "Reindex failed" or similar. |
| 8 | Verify error details are included. | Entry shows error reason (e.g., "401 Unauthorized"). |
| 9 | Verify entry indicates data preservation. | Entry confirms "previous index retained" or similar. |
| 10 | Verify timestamp accuracy. | Timestamp matches failure time. |

## Expected Final State

History contains detailed entry for failed reindex including error cause and data preservation confirmation.

## Pass/Fail Criteria

**Pass:**
- New history entry for failed reindex
- Event type indicates failure
- Error details are specific and helpful
- Data preservation is confirmed
- Timestamp accurate

**Fail:**
- No history entry for failure
- Generic error without details
- No indication of data preservation
- Missing timestamp
