---
id: ELITEA-0085
title: "Pipeline Added as Participant Appears in Autosuggest"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0085: Pipeline Added as Participant Appears in Autosuggest

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a pipeline added via "+ Pipeline" in the Toolkits section appears in the autosuggest with entity type "Pipeline".

**Coverage:** Pipeline entity type in autosuggest; entity type label "Pipeline" shown under item name

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Agent has a pipeline added via "+ Pipeline" button

## Test Data

Pipeline name added to the agent

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent in edit mode, expand Instructions. | Instructions field editable. |
| 2 | Type `/` in the Instructions field. | Autosuggest dropdown appears. |
| 3 | Locate the pipeline entry. | Pipeline name is listed with entity type label "Pipeline". |

## Expected Final State

Pipeline name is listed with entity type label "Pipeline".

## Pass/Fail Criteria

PASS: Pipeline name and "Pipeline" label visible in dropdown
FAIL: Pipeline missing or shown with wrong label
