---
id: ELITEA-3422
title: "ADO search_code: Glob path Argument Does Not Silently Widen OR/NOT Queries"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [feat:ado, tool:search_code, story:6300, path-parameter, glob, boolean-query, regression]
requirements: [EliteaAI/elitea_issues#6300]
---
# ELITEA-3422: search_code path Parameter Glob — Does Not Widen Boolean OR/NOT Queries

**Module:** ADO · **Priority:** High · **Type:** Functional

**Objective:** ADO Code Search parses an unbracketed `A OR B path:x` as `A OR (B AND path:x)` — the inline `path:` token only scopes the term immediately before it, not the whole query. Confirm the fix wraps the caller's original query in parentheses before appending the glob-derived `path:` token, so a `path` argument combined with an `OR`/`NOT` query still scopes the path restriction across the entire boolean expression, not just its last clause.

**Coverage:** Regression — non-obvious edge case verified by the fix's own author; without the parenthesization, a glob `path` argument would silently leak results from outside the intended path whenever combined with `OR`/`NOT`

## Preconditions

- ADO toolkit configured against a project containing the `glob6300` test fixture (`glob6300/src/utils/a.py`, `b.py`, `c.py`, `glob6300/src/helpers/d.py`)
- A second, unrelated token/file outside the `glob6300` folder that also matches part of the query (e.g. a token such as `XQZY_SEARCHTOKEN_9821` present in a file elsewhere in the repo, per the fix's own verification setup)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Call `search_code` with `query="XQZY_SEARCHTOKEN_9821 OR GLOB6300TOKEN"` and `path=glob6300/**`. | Returns only files under `glob6300` (4 files) — the unrelated file matching `XQZY_SEARCHTOKEN_9821` outside `glob6300` is excluded, because the path restriction scopes the whole `OR` expression. |
| 2 | Inspect the result set from step 1 for any file outside `glob6300`. | None present. |

## Expected Final State

Combining a glob `path` argument with a boolean `OR`/`NOT` query restricts results to the given path across the entire query, not just the clause nearest the appended `path:` token.

## Pass/Fail Criteria

**Pass:**
- Step 1 returns exactly the 4 files under `glob6300` and nothing outside it

**Fail:**
- Step 1 also returns file(s) outside `glob6300` that match only the other side of the `OR` (indicates the query wasn't parenthesized before the `path:` token was appended, silently widening the query)
