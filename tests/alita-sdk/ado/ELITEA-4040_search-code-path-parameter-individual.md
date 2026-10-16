---
id: ELITEA-4040
title: "ADO Repos - search_code: path parameter (individual)"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, ado, code-search, issue:6103]
requirements: [EliteaAI/elitea_issues#6103]
---

# ELITEA-4040: ADO Repos - search_code: path parameter (individual)

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the `path` parameter alone restricts results to files under the given repository path, distinct from the `path:` syntax embedded in `query`.

## Preconditions

Repository has a known subfolder containing searchable content (e.g. `/src/services`).

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call `search_code` with a known-matching `query` and `path` set to a known subfolder (e.g. `/src/services`) | Only files under that path are returned |
| 2 | Call the same query with `path` omitted | Results are not restricted to that subfolder (broader result set, or at least not narrower) |

## Expected Final State

`path` correctly narrows results to files under the given folder when set.

## Pass/Fail Criteria

**Pass:**
- path value correctly narrows results to that folder only
- Omitting path returns the unrestricted (broader) result set

**Fail:**
- path parameter is ignored, or results outside the specified path are returned
