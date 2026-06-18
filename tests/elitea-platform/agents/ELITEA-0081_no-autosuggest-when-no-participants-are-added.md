---
id: ELITEA-0081
title: "No Autosuggest When No Participants Are Added"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0081: No Autosuggest When No Participants Are Added

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that typing `/` in Instructions produces no dropdown when the agent has no toolkits, MCPs, agents, or pipelines added.

**Coverage:** Empty participant state; no false dropdown trigger

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Agent with NO participants added (Toolkits section empty or has only Internal Tools)

## Test Data

Agent with empty Toolkits section

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent in edit mode. Confirm the Toolkits section has no added toolkits, MCPs, agents, or pipelines. | No participants listed. |
| 2 | Expand Instructions, click inside the field and type `/`. | No autosuggest dropdown appears. |

## Expected Final State

No autosuggest dropdown appears.

## Pass/Fail Criteria

PASS: No dropdown appears; Instructions field accepts `/` as plain text
FAIL: A dropdown appears (even empty) for an agent with no participants
