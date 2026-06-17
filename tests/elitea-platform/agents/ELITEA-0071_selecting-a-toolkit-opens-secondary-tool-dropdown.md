---
id: ELITEA-0071
title: "Selecting a Toolkit Opens Secondary Tool Dropdown"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0071: Selecting a Toolkit Opens Secondary Tool Dropdown

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting a Toolkit from autosuggest opens a second dropdown listing available tools for that Toolkit.

**Coverage:** Two-level selection flow for Toolkits; tool list populated

## Preconditions

- Agent with a toolkit (e.g., "Ado_repo_M") that has visible tools ("Show tools")

## Test Data

Toolkit: Ado_repo_M

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type `/` in Instructions. | First dropdown appears with participant list. |
| 2 | Click on "Ado_repo_M" from the dropdown. | A second dropdown appears listing the tools of "Ado_repo_M". |
| 3 | Verify the second dropdown contains at least one tool name. | Tool names are listed. |

## Expected Final State

Tool names are listed.

## Pass/Fail Criteria

PASS: Second dropdown appears with tool names after Toolkit selection
FAIL: No second dropdown appears; mention inserted immediately without tool selection
