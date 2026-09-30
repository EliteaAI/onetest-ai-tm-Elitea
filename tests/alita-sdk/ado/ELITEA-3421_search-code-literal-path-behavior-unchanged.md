---
id: ELITEA-3421
title: "ADO search_code: Literal (Non-Glob) path Values Keep Prior Behavior"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [feat:ado, tool:search_code, story:6300, path-parameter, regression]
requirements: [EliteaAI/elitea_issues#6300]
---
# ELITEA-3421: search_code path Parameter — Literal Values Keep Prior Behavior

**Module:** ADO · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm that adding glob support to the `path` argument did not change behavior for callers who pass a literal (non-glob) path — it must still use the whole-subtree, whole-folder-name-only match (no substring/partial match), exactly as before this fix.

**Coverage:** Regression — literal `path` values must continue to route through the REST API's literal `Path` facet, not the query parser

## Preconditions

- ADO toolkit configured against a project containing the `glob6300` test fixture: `glob6300/src/utils/a.py`, `glob6300/src/utils/b.py` and `c.py` at a deeper level, `glob6300/src/helpers/d.py`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `search_code` with `path=glob6300/src` (literal, no wildcard characters). | Returns all 4 files under the subtree (`a.py`, `b.py`, `c.py`, `helpers/d.py`) — over-broad by design, since a literal path matches the whole subtree. |
| 2 | Call `search_code` with `path=glob6300/src/utils` (literal, exact folder). | Returns only `a.py` — the file(s) directly in that exact folder, no partial/substring match against sibling or nested folder names. |

## Expected Final State

Literal `path` values are unaffected by the glob-handling change: same whole-subtree matching, same folder-name-exact semantics as before #6300 was fixed.

## Pass/Fail Criteria

**Pass:**
- `path=glob6300/src` returns all 4 files
- `path=glob6300/src/utils` returns only `a.py`

**Fail:**
- Either literal path call returns a different result set than before this fix (e.g. narrower, broader, or includes files outside the specified folder via unintended partial matching)
