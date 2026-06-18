---
id: ELITEA-0088
title: "Configured MCP Appears in Autosuggest"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0088: Configured MCP Appears in Autosuggest

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a properly configured MCP added to the agent appears in the `/` autosuggest dropdown.

**Coverage:** MCP entity type visible in autosuggest; entity type label "MCP" shown under item name

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Agent has a valid MCP added with successful connection (no "Log in" required)

## Test Data

MCP name added to the agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent in edit mode, expand Instructions. | Instructions field editable. |
| 2 | Type `/` in the Instructions field. | Autosuggest dropdown appears. |
| 3 | Find the MCP entry in the list. | MCP name is listed with entity type label "MCP". |

## Expected Final State

MCP name is listed with entity type label "MCP".

## Pass/Fail Criteria

PASS: MCP name and "MCP" label visible in dropdown
FAIL: MCP missing from dropdown or shown with incorrect label
