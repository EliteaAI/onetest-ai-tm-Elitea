---
id: ELITEA-4043
title: "ADO Repos - search_code: include_snippets parameter (individual)"
priority: medium
type: functional
module: ado
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, ado, code-search, issue:6103]
requirements: [EliteaAI/elitea_issues#6103]
---

# ELITEA-4043: ADO Repos - search_code: include_snippets parameter (individual)

**Module:** Ado · **Priority:** Medium · **Type:** Functional

**Objective:** Verify `include_snippets` alone toggles whether matched code snippets are included in the response.

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call `search_code` with `query` only, `include_snippets` omitted (default true) | Results include a `snippets` array where matches have content |
| 2 | Call the same query with `include_snippets=false` | No `snippets` key on any result; only file metadata is returned |

## Expected Final State

Snippet inclusion in the response matches the `include_snippets` value.

## Pass/Fail Criteria

**Pass:**
- snippets present by default, absent when set to false

**Fail:**
- snippets appear even when include_snippets=false, or never appear by default
