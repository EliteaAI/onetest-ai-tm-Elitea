---
id: ELITEA-4046
title: "ADO Repos - search_code: negative test cases"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, ado, code-search, issue:6103]
requirements: [EliteaAI/elitea_issues#6103]
---

# ELITEA-4046: ADO Repos - search_code: negative test cases

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify `search_code` fails gracefully — no crash, no misleading success — for invalid input and insufficient access.

## Test Data

| Scenario | Input |
|---|---|
| Empty query | `query=""` or `"   "` |
| Non-existent path | `query`=valid, `path="/this/path/does/not/exist"` |
| Non-existent branch | `query`=valid, `branch="does-not-exist-branch"` |
| Insufficient access | valid `query`, token without Code (read) scope, or Stakeholder-access account |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call `search_code` with an empty/whitespace-only query | Returns a `ToolException`, no API call side effects |
| 2 | Call `search_code` with a valid query and a `path` that doesn't exist in the repo | Returns a clean empty result set (`results: []`), no crash |
| 3 | Call `search_code` with a valid query and a `branch` name that doesn't exist | Returns a clean empty result set or a clear error, no crash |
| 4 | Call `search_code` with a token lacking Code (read) scope | Returns a `ToolException`, not a silent empty success or an unhandled crash |

## Expected Final State

Every invalid scenario is handled gracefully — clear exception or clean empty result, never a crash or misleading success.

## Pass/Fail Criteria

**Pass:**
- Every invalid scenario above is handled gracefully with either an empty result or a clear exception — never a crash or misleading success

**Fail:**
- Any scenario crashes the tool, hangs, or returns a misleading/ambiguous result
