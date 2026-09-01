---
id: ELITEA-3082
title: "UI Shows Reindex Failed with Data Preservation Confirmation"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, ui]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3082: UI Shows Reindex Failed with Data Preservation Confirmation

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when reindex fails, the UI displays a clear failure message that confirms previously indexed data remains available for search.

**Coverage:**
- Failure message is displayed
- Message confirms data preservation
- Index card shows appropriate status (not broken)
- History reference for details

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed index
- Ability to cause reindex failure

## Test Data

- Index: Toolkit index with external integration
- Failure method: Token revocation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab, select an existing completed index. | Index displayed. |
| 2 | Cause reindex failure condition. | Condition set. |
| 3 | Initiate Reindex. | Reindex starts, then fails. |
| 4 | Observe the failure notification/message. | Clear "Reindex failed" message displayed. |
| 5 | Verify message content includes: | - |
|   | a) Failure indication | "Reindex failed" or "could not complete". |
|   | b) Data preservation | "Previously indexed data remains available". |
|   | c) Next steps | "Check History for details" or "try again". |
| 6 | Verify index card status. | Shows ✅ (previous status), not ❌ broken. |
| 7 | Verify notification dismisses or persists appropriately. | User can acknowledge the message. |

## Expected Final State

Clear failure message with data preservation confirmation. Index remains in usable state with previous data.

## Pass/Fail Criteria

**Pass:**
- Failure message clearly displayed
- Data preservation explicitly confirmed
- Guidance on next steps provided
- Index card shows healthy status

**Fail:**
- No clear failure indication
- No confirmation of data preservation
- User left confused about index state
- Index appears broken in UI
