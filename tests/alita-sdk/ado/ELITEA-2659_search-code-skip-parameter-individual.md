---
id: ELITEA-2659
title: "ADO Repos - search_code: skip parameter (individual)"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, ado, code-search, issue:6103]
requirements: [EliteaAI/elitea_issues#6103]
---

# ELITEA-2659: ADO Repos - search_code: skip parameter (individual)

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the `skip` parameter alone pages past earlier results without duplication.

## Preconditions

Query is known to match more than 10 files in the repository.

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call `search_code` with `query` only, `skip=0` (or omitted) | First page of results returned |
| 2 | Call the same query with `skip=5` | A different, non-overlapping set of results is returned |

## Expected Final State

`skip` correctly advances the result window with no overlap between pages.

## Pass/Fail Criteria

**Pass:**
- skip correctly advances past previously returned results with no duplicates

**Fail:**
- skip is ignored, or the same results repeat
