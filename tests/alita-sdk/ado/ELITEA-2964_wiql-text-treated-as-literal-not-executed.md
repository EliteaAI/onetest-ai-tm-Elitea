---
id: ELITEA-2964
title: "ADO Work Item Text Search – WIQL-Shaped Text Is Treated as Literal Search Text, Never Executed as WIQL"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [sdk, ado, toolkit, work-items, text-search, issue:6104]
requirements: [EliteaAI/elitea_issues#6104]
---

# ELITEA-2964: ADO Work Item Text Search – WIQL-Shaped Text Is Treated as Literal Search Text, Never Executed as WIQL

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify passing a WIQL-style string as `query` is treated as literal free text for the search index, not parsed/executed as a WIQL query.

---

## Preconditions

- ADO Board toolkit is configured with valid credentials.

---

## Test Data

| Field | Value |
|-------|-------|
| query | `SELECT * FROM WorkItems WHERE [System.TeamProject] = '@project'` |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Call `search_work_items_by_text` with the WIQL string above as `query` | Call succeeds without a WIQL syntax/execution error |
| 2 | Inspect returned results | Results (if any) reflect a literal free-text match against the search index, not a WIQL result set |

---

## Expected Final State

The tool never attempts to execute the input as WIQL; it is always passed through as search text.

---

## Pass/Fail Criteria

**Pass:** No WIQL execution occurs; the string is handled purely as search text.
**Fail:** The tool attempts to parse/execute the string as WIQL, producing a WIQL-specific error or a WIQL-shaped result set.
