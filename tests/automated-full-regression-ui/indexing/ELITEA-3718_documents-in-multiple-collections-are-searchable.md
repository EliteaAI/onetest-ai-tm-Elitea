---
id: ELITEA-3718
title: "Verify documents in multiple collections are searchable in all collections"
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
- User has two indexes configured that include overlapping documents

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/{{project_id}}/configuration/toolkits` |
| Index A | First index including shared document |
| Index B | Second index including same shared document |
| Shared document | Document that exists in both index sources |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create Index A including the shared document | Index A created successfully |
| 2 | Create Index B including the same document | Index B created successfully |
| 3 | Search using Index A for the shared document | Document is found |
| 4 | Search using Index B for the shared document | Document is found |
| 5 | Verify document count in both indexes | Document is counted in both indexes |

## Expected Final State

The shared document is searchable and counted correctly in both indexes.

## Pass/Fail Criteria

**Pass:**
- Document appears in search results for both Index A and Index B
- Document is counted in both indexes

**Fail:**
- Document is missing from one or both index searches
- Document count is incorrect in either index
