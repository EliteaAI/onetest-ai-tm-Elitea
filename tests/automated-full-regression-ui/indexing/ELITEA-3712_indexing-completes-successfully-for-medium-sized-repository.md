---
id: ELITEA-3712
title: "Verify indexing completes successfully for medium-sized repository"
priority: critical
type: functional
module: indexes
status: draft
execution_type: manual
tags: [feat:indexer, eng:technical-debt, r-2.0.7]
requirements: [EliteaAI/elitea_issues#6228]
---

## Preconditions

- User is logged in to `{{base_url}}`
- User has access to a project with a configured toolkit (GitHub/Confluence/SharePoint)
- Data source contains 100-500 documents

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Source type | GitHub repository / Confluence space / SharePoint site |
| Document count | 100-500 items |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits > Indexes | Indexes list page displays |
| 2 | Click "Create Index" for configured toolkit | Index creation dialog opens |
| 3 | Configure index settings and click "Start Indexing" | Indexing process starts, status shows "in_progress" |
| 4 | Wait for indexing to complete | Status changes to "completed" |
| 5 | Check indexed document count | Count matches expected number of documents |

## Expected Final State

Index status is "completed" with correct document count displayed.

## Pass/Fail Criteria

**Pass:**
- Index status shows "completed"
- Indexed count matches source document count
- No errors displayed

**Fail:**
- Index status remains "in_progress" indefinitely
- Status shows "failed" without valid reason
- Document count is zero or incorrect
