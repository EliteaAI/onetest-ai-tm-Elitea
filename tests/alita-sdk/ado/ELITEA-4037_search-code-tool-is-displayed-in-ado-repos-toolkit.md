---
id: ELITEA-4037
title: "ADO Repos - search_code: Tool is displayed/available in the toolkit"
priority: high
type: functional
module: ado
status: draft
execution_type: manual
tags: [repository, toolkit, sdk, ado, code-search, issue:6103]
requirements: [EliteaAI/elitea_issues#6103]
---

# ELITEA-4037: ADO Repos - search_code: Tool is displayed/available in the toolkit

**Module:** Ado · **Priority:** High · **Type:** Functional

**Objective:** Verify the new `search_code` tool is visible/selectable in the ADO Repos toolkit's tool list and reported by `get_available_tools()`.

## Preconditions

ADO Repos toolkit is configured against a Git repository.

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the ADO Repos toolkit configuration/tool selection UI | `search_code` (or its display name) appears in the list of available tools alongside existing ADO Repos tools |
| 2 | Call `get_available_tools()` on the toolkit | `search_code` is present in the returned list with a name and description |

## Expected Final State

`search_code` is listed as an available tool in both the UI and `get_available_tools()`.

## Pass/Fail Criteria

**Pass:**
- search_code is listed in the toolkit configuration UI
- search_code is present in get_available_tools()

**Fail:**
- search_code is missing from either location
