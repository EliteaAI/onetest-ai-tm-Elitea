---
id: ELITEA-0089
title: "Autosuggest Triggers on `/` in Instructions Editor Only"
priority: critical
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0089: Autosuggest Triggers on `/` in Instructions Editor Only

**Module:** Agents · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that typing `/` in the Instructions text field opens the autosuggest dropdown, and that it does NOT trigger in any other field.

**Coverage:** Trigger in Instructions field; no trigger in Description, Welcome Message, Conversation Starters fields

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Agent exists with at least one valid Toolkit, MCP, Agent, and Pipeline added

## Test Data

Any agent with at least one valid configured participant

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents → open an existing agent → expand Instructions section. | Instructions text field is visible and editable. |
| 2 | Click inside the Instructions field and type `/`. | An autosuggest dropdown appears immediately below the cursor. |
| 3 | Press Backspace, click into the Description field, type `/`. | No dropdown appears. |
| 4 | Click into the Welcome Message field, type `/`. | No dropdown appears. |
| 5 | Click into the Conversation Starters field, type `/`. | No dropdown appears. |

## Expected Final State

No dropdown appears.

## Pass/Fail Criteria

PASS: Dropdown appears only in the Instructions field; all other fields ignore `/`
FAIL: Dropdown appears in any non-Instructions field; dropdown fails to appear in Instructions field
