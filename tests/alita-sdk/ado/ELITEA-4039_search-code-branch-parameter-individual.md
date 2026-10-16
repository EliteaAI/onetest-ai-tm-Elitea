---
id: ELITEA-4039
title: "ADO Repos - search_code: branch parameter (individual)"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, ado, code-search, issue:6103]
requirements: [EliteaAI/elitea_issues#6103]
---

# ELITEA-4039: ADO Repos - search_code: branch parameter (individual)

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the `branch` parameter alone restricts search results to the specified branch.

## Preconditions

Know the repository's indexed default branch.

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call `search_code` with a known-matching `query` and `branch` set to the default branch, no other params set | Results returned, all attributed to that branch |
| 2 | Call `search_code` with the same `query` and `branch` omitted | Results returned from the default indexed branch (no behavior change vs. step 1) |

## Expected Final State

`branch` correctly scopes results to the given branch when set, and defaults sensibly when omitted.

## Pass/Fail Criteria

**Pass:**
- branch value correctly restricts/labels results
- Omitting branch behaves the same as passing the default branch

**Fail:**
- branch parameter is ignored or results are attributed to the wrong branch
