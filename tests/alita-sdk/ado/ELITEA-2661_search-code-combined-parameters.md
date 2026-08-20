---
id: ELITEA-2661
title: "ADO Repos - search_code: combined parameters"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, ado, code-search, issue:6103]
requirements: [EliteaAI/elitea_issues#6103]
---

# ELITEA-2661: ADO Repos - search_code: combined parameters

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify `search_code` behaves correctly when 2-3 parameters are supplied together, not just individually, with no parameter overriding or being dropped by another.

## Test Data

| Combination | Params | Expectation |
|---|---|---|
| 1 | `query`, `path`, `top=3` | Results limited to the given path AND capped at 3 files |
| 2 | `query`, `branch`, `include_snippets=false` | Results limited to the given branch AND metadata-only (no snippets) |
| 3 | `query`, `path`, `top=3`, `skip=3` | Results limited to the given path, second page (files 4-6) |

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Call `search_code` with combination 1 | Both the path restriction and the top=3 cap are honored simultaneously |
| 2 | Call `search_code` with combination 2 | Both the branch restriction and the no-snippets behavior are honored simultaneously |
| 3 | Call `search_code` with combination 3 | Path restriction honored, and results are the second page (skip=3) within that restricted set, not the first page of the unrestricted set |

## Expected Final State

All parameters in each combination apply together correctly with no interference between them.

## Pass/Fail Criteria

**Pass:**
- All parameters in each combination apply together correctly, with no parameter overriding or being dropped by another

**Fail:**
- Any parameter in a combination is ignored, or combining parameters produces incorrect/unexpected results
