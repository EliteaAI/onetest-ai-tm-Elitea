---
id: ELITEA-0070
title: "Selecting a Tool Formats Mention as `/Toolkit#tool`"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0070: Selecting a Tool Formats Mention as `/Toolkit#tool`

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that selecting a tool after a Toolkit inserts the mention in `/ToolkitName#toolName` format.

**Coverage:** Correct mention format with tool suffix; highlight applied

## Preconditions

- Agent with a configured Toolkit (e.g., "Ado_repo_M") with at least one visible tool

## Test Data

Toolkit: Ado_repo_M; tool: any available tool name; expected format: /Ado_repo_M#toolName

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type `/` in Instructions, select "Ado_repo_M". | Second tool dropdown appears. |
| 2 | Select the first available tool from the second dropdown. | Mention inserted as /Ado_repo_M#<toolName> in bold blue. |

## Expected Final State

Mention inserted as /Ado_repo_M#<toolName> in bold blue.

## Pass/Fail Criteria

PASS: Inserted text matches /Ado_repo_M#toolName format and is highlighted
FAIL: Format wrong (missing #, missing tool name, or plain text instead of highlighted)
