---
id: ELITEA-0087
title: "Sub-Agent Added as Participant Appears in Autosuggest"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0087: Sub-Agent Added as Participant Appears in Autosuggest

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an agent added via "+ Agent" in the Toolkits section appears in the autosuggest with entity type "Agent".

**Coverage:** Agent entity type in autosuggest; entity type label "Agent" shown under item name

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Agent has a sub-agent (e.g., "planner") added via "+ Agent" button, showing a version selector

## Test Data

Sub-agent name: planner

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent in edit mode, expand Instructions. | Instructions field editable. |
| 2 | Type `/` in the Instructions field. | Autosuggest dropdown appears. |
| 3 | Locate the sub-agent entry. | "planner" is listed with entity type label "Agent". |

## Expected Final State

"planner" is listed with entity type label "Agent".

## Pass/Fail Criteria

PASS: Sub-agent name and "Agent" label visible in dropdown
FAIL: Sub-agent missing from dropdown or shown with wrong label
