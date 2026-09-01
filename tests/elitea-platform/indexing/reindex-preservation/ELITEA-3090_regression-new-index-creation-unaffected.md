---
id: ELITEA-3090
title: "Regression: New Index Creation Flow Unaffected"
priority: medium
type: regression
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, regression]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3090: Regression: New Index Creation Flow Unaffected

**Module:** Indexing · **Priority:** Medium · **Type:** Regression

**Objective:** Verify that the enhancement for reindex preservation does not negatively impact the existing new index creation flow.

**Coverage:**
- New index creation still works as before
- No unintended side effects from reindex enhancement
- Index becomes active upon successful initial creation
- All index features work for newly created indexes

## Preconditions

- Logged in to {{base_url}}
- Ability to create a new index
- Valid integration credentials for the toolkit

## Test Data

- Toolkit: Any configured toolkit (Artifacts, Confluence, GitHub, etc.)
- Source: Valid data source with content to index

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab. Click "Create Index" or equivalent. | Create index form displayed. |
| 2 | Configure new index with valid settings and credentials. | Configuration accepted. |
| 3 | Start indexing. | Indexing begins, status shows "In Progress". |
| 4 | Wait for indexing to complete. | Status shows ✅ Completed. |
| 5 | Verify document count is > 0. | Documents indexed (e.g., 30 docs). |
| 6 | Verify "Last indexed" timestamp is current. | Timestamp shows current time. |
| 7 | Perform a search on the new index. | Search returns results. |
| 8 | Verify index card shows correct status. | Card shows ✅ Completed with count. |
| 9 | Verify Index History shows creation event. | History entry for initial indexing exists. |
| 10 | Initiate Reindex on the new index. Wait for completion. | Reindex completes successfully. |

## Expected Final State

New index creation flow works exactly as before the enhancement. No regressions introduced.

## Pass/Fail Criteria

**Pass:**
- New index creation completes successfully
- Index becomes active with searchable content
- All index features work (search, history, reindex)
- No unexpected errors or behaviors

**Fail:**
- New index creation fails or behaves differently
- Index not searchable after creation
- Features broken for new indexes
- Unexpected side effects from enhancement
