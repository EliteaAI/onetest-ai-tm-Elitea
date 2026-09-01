---
id: ELITEA-3078
title: "Network/Service Error Shows Clear Guidance Message"
priority: high
type: functional
module: indexing
status: ready
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, error-handling]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3078: Network/Service Error Shows Clear Guidance Message

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when reindex fails due to network issues or service unavailability, the error message is clear and confirms that previously indexed data remains available.

**Coverage:**
- Error message indicates service/network issue
- Message confirms previous data remains available
- User is guided to retry after resolving the issue

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed index connected to external service
- Ability to simulate network failure or service unavailability

## Test Data

- Index: Any toolkit index with external dependency
- Action: Block network access to external service or wait for service maintenance window

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab, select an existing completed index. | Index selected. |
| 2 | Simulate network issue (e.g., disconnect VPN, block external host). | Network to external service blocked. |
| 3 | Initiate Reindex. | Reindex starts and then fails. |
| 4 | Observe the error notification/message. | Message indicates service/network unavailability. |
| 5 | Verify message confirms data preservation. | Message states: "Previously indexed data remains available for search". |
| 6 | Verify index status. | Index shows previous Completed status. |
| 7 | Restore network connectivity. | Network restored. |
| 8 | Verify search still works. | Search returns results from active index. |

## Expected Final State

Clear error message about connectivity issue. Previous index data remains fully accessible.

## Pass/Fail Criteria

**Pass:**
- Error message indicates network/service issue
- Data preservation confirmed in message
- Index status unchanged
- Search works after failure

**Fail:**
- Cryptic or unhelpful error message
- No confirmation of data preservation
- Index marked as failed/broken
- Search fails after network error
