---
id: ELITEA-3088
title: "Retry Reindex After Fixing Credentials"
priority: medium
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, recovery]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3088: Retry Reindex After Fixing Credentials

**Module:** Indexing · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after a reindex failure due to authentication issues, the user can fix credentials and successfully reindex without data loss.

**Coverage:**
- Recovery workflow after credential failure
- Successful reindex after credential fix
- New index replaces active index upon success
- Previous data available throughout recovery process

## Preconditions

- Logged in to {{base_url}}
- An existing ✅ Completed index with external integration
- Ability to revoke and restore credentials

## Test Data

- Index: Toolkit index with OAuth or token authentication
- Search query: Known content in the index

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab, select an index. Verify search works. | Search returns results (e.g., 25 documents). |
| 2 | Revoke/invalidate the integration credentials. | Credentials invalidated. |
| 3 | Initiate Reindex. Wait for failure. | Reindex fails with 401 error. |
| 4 | Verify search still works with previous data. | Search returns same 25 documents. |
| 5 | Restore/reconnect the integration credentials. | Credentials restored. |
| 6 | Initiate Reindex again. | Reindex starts. |
| 7 | Wait for successful completion. | ✅ Completed. |
| 8 | Verify search works with newly indexed data. | Search returns results (count may differ). |
| 9 | Verify "Last indexed" timestamp is updated. | Shows current time. |

## Expected Final State

After credential fix, reindex completes successfully. New index is active. Data was available throughout the recovery process.

## Pass/Fail Criteria

**Pass:**
- Previous data remained available during entire recovery
- Reindex succeeds after credential fix
- New index becomes active
- No data loss at any point

**Fail:**
- Data unavailable during recovery
- Reindex still fails after credential fix
- Old data persists despite successful reindex
- Data loss occurred
