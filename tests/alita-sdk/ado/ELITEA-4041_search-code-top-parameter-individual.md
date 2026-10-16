---
id: ELITEA-4041
title: "ADO Repos - search_code: top parameter (individual)"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, ado, code-search, issue:6103]
requirements: [EliteaAI/elitea_issues#6103]
---

# ELITEA-4041: ADO Repos - search_code: top parameter (individual)

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the `top` parameter alone controls how many files are returned, with correct default and clamping behavior.

## Preconditions

Query is known to match more than 10 files in the repository.

## Test Data

| `top` value | Expected `returned` |
|---|---|
| (unset) | ≤ 5 (default) |
| 10 | ≤ 10 |
| 10000 | ≤ 1000 (clamped to service max) |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call `search_code` with only `query` set, `top` unset | `returned` ≤ 5 (default) |
| 2 | Call the same query with `top=10` | `returned` ≤ 10 |
| 3 | Call the same query with `top=10000` | `returned` ≤ 1000 (clamped to service max, not rejected with an error) |

## Expected Final State

`returned` count reflects the requested (or clamped) `top` value in every case.

## Pass/Fail Criteria

**Pass:**
- returned count matches expectation for default, custom, and clamped top values

**Fail:**
- top is ignored, or an out-of-range value is passed through unclamped
