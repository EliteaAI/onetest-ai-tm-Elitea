---
id: ELITEA-3420
title: "ADO search_code: path Parameter Glob Matches Equivalent Inline path: Query Filter"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [feat:ado, tool:search_code, story:6300, path-parameter, glob, parity]
requirements: [EliteaAI/elitea_issues#6300]
---
# ELITEA-3420: search_code path Parameter Glob — Parity with Inline path: Query Filter

**Module:** ADO · **Priority:** High · **Type:** Functional

**Objective:** Confirm that a glob pattern passed via the dedicated `path` argument returns exactly the same result set as writing the identical pattern as an inline `path:` token in the `query` string, for both a mid-tree wildcard (variable-depth named folder) and a root-anchored wildcard (broadened search).

**Coverage:** AC — `path` argument achieves parity with the pre-existing inline `path:` query syntax for glob patterns

## Preconditions

- ADO toolkit configured against a project containing the `glob6300` test fixture: `glob6300/src/utils/a.py`, `glob6300/src/utils/b.py`, `glob6300/src/utils/c.py` at a deeper level, and `glob6300/src/helpers/d.py`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `search_code` with `path=glob6300/src/**/utils` (named folder at variable depth). | Returns `b.py` and `c.py` (2 results). |
| 2 | Call `search_code` with `query` containing the inline filter `path:glob6300/src/**/utils` instead of the `path` argument. | Returns the identical 2 results (`b.py`, `c.py`) as step 1. |
| 3 | Call `search_code` with `path=glob6300/**/utils` (broadened, anchored at the fixture root). | Returns `a.py`, `b.py`, and `c.py` (3 results). |
| 4 | Call `search_code` with `query` containing the inline filter `path:glob6300/**/utils` instead of the `path` argument. | Returns the identical 3 results (`a.py`, `b.py`, `c.py`) as step 3. |

## Expected Final State

For any glob pattern, using the dedicated `path` argument produces the exact same result set as embedding the same pattern as an inline `path:` filter in the query string — the two entry points are functionally equivalent.

## Pass/Fail Criteria

**Pass:**
- `path=glob6300/src/**/utils` and inline `path:glob6300/src/**/utils` both return exactly `b.py`, `c.py`
- `path=glob6300/**/utils` and inline `path:glob6300/**/utils` both return exactly `a.py`, `b.py`, `c.py`

**Fail:**
- The `path` argument and the equivalent inline `path:` filter return different result counts or different files for the same pattern
