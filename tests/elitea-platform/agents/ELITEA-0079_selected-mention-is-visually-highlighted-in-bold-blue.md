---
id: ELITEA-0079
title: "Selected Mention Is Visually Highlighted in Bold Blue"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0079: Selected Mention Is Visually Highlighted in Bold Blue

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that any inserted mention (Toolkit, MCP, Agent, Pipeline) is rendered in bold with blue font color in the Instructions editor.

**Coverage:** Visual highlight for all four entity types; bold + blue font

## Preconditions

- Agent with at least one participant of each type (Toolkit, MCP, Agent, Pipeline)

## Test Data

One participant of each type

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type `/` and select a Toolkit. | Inserted mention is bold and blue. |
| 2 | Type `/` again and select an MCP. | Inserted mention is bold and blue. |
| 3 | Type `/` again and select an Agent. | Inserted mention is bold and blue. |
| 4 | Type `/` again and select a Pipeline. | Inserted mention is bold and blue. |

## Expected Final State

Inserted mention is bold and blue.

## Pass/Fail Criteria

PASS: All four entity type mentions are bold and blue in the Instructions editor
FAIL: Any mention is plain text (no bold or no blue); styling differs across entity types
