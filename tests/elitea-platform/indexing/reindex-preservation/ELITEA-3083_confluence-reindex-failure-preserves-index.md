---
id: ELITEA-3083
title: "Confluence Reindex Failure Preserves Active Index"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, confluence]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3083: Confluence Reindex Failure Preserves Active Index

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when Confluence reindex fails (e.g., due to expired OAuth session), the previously indexed Confluence data remains searchable.

**Coverage:**
- Confluence-specific reindex failure handling
- OAuth session expiration scenario
- Data preservation for Confluence indexes
- Clear error about session/reconnection

## Preconditions

- Logged in to {{base_url}}
- Confluence integration connected via OAuth
- An existing ✅ Completed Confluence index with searchable content

## Test Data

- Index: Confluence space index
- Searchable content: Known page title or content keyword
- Failure method: Wait for OAuth session expiration or revoke token in Confluence

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab, select Confluence index. | Index displayed with document count. |
| 2 | Search for known Confluence content. Note results. | Results returned (e.g., 5 pages). |
| 3 | Cause OAuth session to expire or revoke access in Confluence. | Session invalidated. |
| 4 | Initiate Reindex on Confluence index. | Reindex starts, then fails. |
| 5 | Verify error message mentions authentication/session. | Error indicates session expired or unauthorized. |
| 6 | Verify error suggests reconnecting. | Message guides to reconnect Confluence. |
| 7 | Search for the same Confluence content again. | Same 5 pages returned as before. |
| 8 | Verify index status shows ✅ Completed. | Status unchanged from before failure. |

## Expected Final State

Confluence index remains fully searchable with all previously indexed pages. Clear guidance provided to reconnect.

## Pass/Fail Criteria

**Pass:**
- Confluence data remains searchable after failure
- Error clearly indicates authentication issue
- Guidance to reconnect is provided
- Index status shows completed

**Fail:**
- Confluence search fails or returns no results
- Generic error without Confluence-specific guidance
- Index marked as broken
- Data lost
