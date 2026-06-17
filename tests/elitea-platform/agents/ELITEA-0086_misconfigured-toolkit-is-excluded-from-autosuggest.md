---
id: ELITEA-0086
title: "Misconfigured Toolkit Is Excluded from Autosuggest"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, Bug:5011, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0086: Misconfigured Toolkit Is Excluded from Autosuggest

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a toolkit with broken/invalid configuration does NOT appear in the autosuggest dropdown.

**Coverage:** Misconfigured toolkit excluded; valid toolkits still shown

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Agent has: one valid Toolkit AND one misconfigured Toolkit (e.g., invalid credentials, health indicator red)

## Test Data

Valid toolkit name (e.g., Ado_repo_M); misconfigured toolkit name (e.g., %%%%)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the agent in edit mode. Confirm the Toolkits section shows both a valid and a misconfigured toolkit. | Both are listed in the Toolkits section. |
| 2 | Expand Instructions, click inside the field and type `/`. | Autosuggest dropdown appears. |
| 3 | Inspect the dropdown list for the misconfigured toolkit. | The misconfigured toolkit does NOT appear. Valid toolkit does appear. |

## Expected Final State

The misconfigured toolkit does NOT appear. Valid toolkit does appear.

## Pass/Fail Criteria

PASS: Misconfigured toolkit absent; valid toolkit present
FAIL: Misconfigured toolkit appears in the dropdown
