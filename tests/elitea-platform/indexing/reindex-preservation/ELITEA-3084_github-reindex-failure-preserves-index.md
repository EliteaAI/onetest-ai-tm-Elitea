---
id: ELITEA-3084
title: "GitHub Reindex Failure Preserves Active Index"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:6232, reindex-preservation, github]
requirements: [EliteaAI/elitea_issues#6232]
---
# ELITEA-3084: GitHub Reindex Failure Preserves Active Index

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when GitHub reindex fails (e.g., due to token expiration or insufficient permissions), the previously indexed GitHub data remains searchable.

**Coverage:**
- GitHub-specific reindex failure handling
- Token expiration/permission scenario
- Data preservation for GitHub indexes
- Clear error about token/permissions

## Preconditions

- Logged in to {{base_url}}
- GitHub integration connected via Personal Access Token
- An existing ✅ Completed GitHub index with searchable content

## Test Data

- Index: GitHub repository index
- Searchable content: Known file name or code snippet
- Failure method: Revoke token or change repository permissions

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Indexes tab, select GitHub index. | Index displayed with document count. |
| 2 | Search for known GitHub content (filename or code). Note results. | Results returned (e.g., 10 files). |
| 3 | Revoke GitHub token or remove repository access permissions. | Token/permissions invalidated. |
| 4 | Initiate Reindex on GitHub index. | Reindex starts, then fails. |
| 5 | Verify error message mentions token or permissions. | Error indicates token expired or permission denied. |
| 6 | Verify error suggests updating token/permissions. | Message guides to update GitHub connection. |
| 7 | Search for the same GitHub content again. | Same 10 files returned as before. |
| 8 | Verify index status shows ✅ Completed. | Status unchanged from before failure. |

## Expected Final State

GitHub index remains fully searchable with all previously indexed files. Clear guidance provided to update token/permissions.

## Pass/Fail Criteria

**Pass:**
- GitHub data remains searchable after failure
- Error clearly indicates token/permission issue
- Guidance to update credentials is provided
- Index status shows completed

**Fail:**
- GitHub search fails or returns no results
- Generic error without GitHub-specific guidance
- Index marked as broken
- Data lost
