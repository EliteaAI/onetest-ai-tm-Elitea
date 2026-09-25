---
id: ELITEA-3419
title: "ADO search_code: path Parameter with ** Glob No Longer Returns 0 Results"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [feat:ado, tool:search_code, story:6300, path-parameter, glob, regression]
requirements: [EliteaAI/elitea_issues#6300]
---
# ELITEA-3419: search_code path Parameter — ** Glob No Longer Returns 0 Results

**Module:** ADO · **Priority:** High · **Type:** Functional

**Objective:** Confirm the original bug reported in #6300 is fixed — passing a `**` glob pattern in the dedicated `path` argument of `search_code` returns results (routed through the query parser as an inline `path:` token) instead of silently returning 0, and that the recursive trailing-`**` case matches its literal-prefix equivalent in result count/content.

**Coverage:** Bug fix — `path` argument previously used the ADO REST API's literal-only `Path` facet, which cannot express wildcards and silently matched nothing for any value containing `*`

## Preconditions

- ADO toolkit configured against a project containing the `glob6300` test fixture folder (`glob6300/src/utils/a.py`, `glob6300/src/helpers/d.py`, plus `b.py`, `c.py`, per the merged fix's own verification)
- A folder such as `testcode` (or equivalent) with exactly one file, for the original issue repro

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `search_code` with `path=/testcode/**`. | Returns 1 result — the same file(s) as passing the literal `path=/testcode`. Previously returned 0 results (the bug). |
| 2 | Call `search_code` with `path=glob6300/src/**` (trailing recursive glob). | Returns all 4 files under `glob6300/src`, including the nested `glob6300/src/helpers/d.py`. |
| 3 | Call `search_code` with the equivalent literal path `path=glob6300/src` (no glob) as a sanity comparison for step 2. | Returns the same 4 files — confirms the glob and literal forms agree when the glob simply expresses "this subtree and everything below it." |

## Expected Final State

`path` values containing `**` return results, matching what the equivalent literal prefix already returns for a fully-recursive pattern.

## Pass/Fail Criteria

**Pass:**
- `path=/testcode/**` returns 1 result (not 0)
- `path=glob6300/src/**` returns all 4 files, matching the literal `glob6300/src` result set

**Fail:**
- Any `path` value containing `**` still returns 0 results
- The `**`-suffixed path returns a different file set than its literal-prefix equivalent
