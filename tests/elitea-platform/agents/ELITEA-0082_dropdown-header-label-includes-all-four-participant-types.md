---
id: ELITEA-0082
title: "Dropdown Header Label Includes All Four Participant Types"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0082: Dropdown Header Label Includes All Four Participant Types

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the autosuggest popup header reads "MENTION TOOLKIT, MCP, AGENT OR PIPELINE".

**Coverage:** UI label correctness; no truncation to "MENTION TOOLKIT OR MCP"

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Agent with at least one Toolkit, MCP, Agent, and Pipeline added and configured

## Test Data

Agent with all four participant types added

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the agent's Instructions field and click inside it. | Instructions field is focused. |
| 2 | Type `/`. | Autosuggest dropdown appears. |
| 3 | Read the header text of the dropdown. | Header reads exactly "MENTION TOOLKIT, MCP, AGENT OR PIPELINE". |

## Expected Final State

Header reads exactly "MENTION TOOLKIT, MCP, AGENT OR PIPELINE".

## Pass/Fail Criteria

PASS: Header text matches "MENTION TOOLKIT, MCP, AGENT OR PIPELINE" exactly
FAIL: Header reads "MENTION TOOLKIT OR MCP" or any other incomplete label
