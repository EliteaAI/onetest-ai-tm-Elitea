---
id: ELITEA-0077
title: "Agent Mention Inserted Directly Without Tool Dropdown"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0077: Agent Mention Inserted Directly Without Tool Dropdown

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting an Agent from autosuggest inserts the mention immediately without showing a secondary tool dropdown.

**Coverage:** No two-level selection for Agents; direct insertion

## Preconditions

- Agent with a sub-agent (e.g., "planner") added

## Test Data

Sub-agent name: planner; expected inserted text: /planner

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type `/` in Instructions. | Dropdown appears showing "planner" with label "Agent". |
| 2 | Click on "planner". | Mention /planner inserted immediately; no second dropdown appears. |
| 3 | Verify the inserted mention is highlighted in bold blue. | Correct format and highlighting applied. |

## Expected Final State

Correct format and highlighting applied.

## Pass/Fail Criteria

PASS: /planner inserted without secondary dropdown; bold blue highlight applied
FAIL: Secondary tool dropdown appears after selecting an agent; no insertion occurs
