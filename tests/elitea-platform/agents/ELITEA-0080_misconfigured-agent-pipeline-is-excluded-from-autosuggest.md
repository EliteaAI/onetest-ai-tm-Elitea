---
id: ELITEA-0080
title: "Misconfigured Agent/Pipeline Is Excluded from Autosuggest"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0080: Misconfigured Agent/Pipeline Is Excluded from Autosuggest

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that an invalid or broken agent/pipeline participant is excluded from autosuggest.

**Coverage:** Invalid agent/pipeline excluded; valid ones shown

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Agent has a sub-agent/pipeline in invalid/broken state alongside a valid one

## Test Data

Valid sub-agent name; invalid sub-agent/pipeline name

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent in edit mode. Confirm there is at least one invalid and one valid participant. | Both visible in Toolkits section. |
| 2 | Expand Instructions, type `/`. | Autosuggest dropdown appears. |
| 3 | Verify the invalid participant is not listed. | Invalid participant absent; valid one present. |

## Expected Final State

Invalid participant absent; valid one present.

## Pass/Fail Criteria

PASS: Invalid agent/pipeline excluded from dropdown
FAIL: Invalid agent/pipeline visible in dropdown
