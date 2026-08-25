---
id: ELITEA-2662
title: "ADO Repos - search_code: search across multiple Searchable branches"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, ado, code-search, issue:6103]
requirements: [EliteaAI/elitea_issues#6103]
---

# ELITEA-2662: ADO Repos - search_code: search across multiple Searchable branches

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify code search works correctly for branches other than the default, as long as they are listed under Project Settings → Repositories → Options → Searchable branches, with correct branch attribution per result.

## Preconditions

At least 2 branches (default branch + one additional branch) added under Searchable branches, each with some distinguishing content.

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Add/confirm a second branch is listed under Searchable branches, with content unique to that branch | Branch is configured for indexing |
| 2 | Call `search_code` with `branch` = the default branch, query matching default-branch-only content | Results returned, correctly attributed to the default branch |
| 3 | Call `search_code` with `branch` = the second Searchable branch, query matching that branch's unique content | Results returned, correctly attributed to the second branch |
| 4 | Repeat step 3 for a third Searchable branch if available | Results returned and correctly attributed |

## Expected Final State

Every branch listed under Searchable branches is searchable and results are attributed to the correct branch.

## Pass/Fail Criteria

**Pass:**
- Every branch listed under Searchable branches can be searched and results are correctly attributed to it

**Fail:**
- A Searchable branch returns no results despite having indexed content, or results are attributed to the wrong branch
