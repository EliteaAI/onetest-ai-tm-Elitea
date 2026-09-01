---
id: ELITEA-3087
title: "First-Time Indexing Failure Handling (No Previous Index)"
priority: medium
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, edge-case]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3087: First-Time Indexing Failure Handling (No Previous Index)

**Module:** Indexing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when initial indexing (not reindexing) fails, the system clearly indicates no indexed data is available without false "previous index retained" messaging.

**Coverage:**
- First-time indexing failure scenario
- No false "previous index retained" message
- Clear indication that no data is available
- User guided to resolve and retry

## Preconditions

- Logged in to {{base_url}}
- Ability to create a new index configuration
- Ability to cause indexing failure (invalid credentials, etc.)

## Test Data

- New index: Create new index with invalid credentials
- Toolkit: Any external integration (Confluence, GitHub, etc.)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab, click "Create Index". | Create index form displayed. |
| 2 | Configure new index with intentionally invalid credentials. | Configuration saved. |
| 3 | Start initial indexing. | Indexing starts, then fails. |
| 4 | Observe the error message. | Error indicates why indexing failed. |
| 5 | Verify message does NOT say "previous index retained". | No false retention message shown. |
| 6 | Verify message indicates no data is available. | States "no indexed data available" or similar. |
| 7 | Verify user is guided to resolve and retry. | Message suggests fixing credentials and retrying. |
| 8 | Verify index card status. | Shows failed/no data status (not ✅ Completed). |

## Expected Final State

Clear messaging that initial indexing failed and no previous data exists. User guided to fix issue and retry.

## Pass/Fail Criteria

**Pass:**
- No false "previous index retained" message
- Clear indication of failure with no data
- Guidance to resolve and retry
- Index status correctly shows no data

**Fail:**
- Message falsely claims previous data retained
- Unclear about data availability
- No guidance on resolution
- Index status misleading
