---
id: ELITEA-0078
title: "Tool Selection Is Optional — Toolkit Mention Inserted Without Tool"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [user_story:3396, feat:agents, r-2.0.3, 3396]
requirements: [EliteaAI/elitea_issues#3396]
---
# ELITEA-0078: Tool Selection Is Optional — Toolkit Mention Inserted Without Tool

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that a user can skip tool selection after choosing a Toolkit and the mention is inserted as `/ToolkitName`.

**Coverage:** Optional tool selection; mention format without tool name

## Preconditions

- Agent with a configured Toolkit that has tools

## Test Data

Toolkit: Ado_repo_M; expected inserted text: /Ado_repo_M

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type `/` in Instructions, select "Ado_repo_M". | Second dropdown with tools appears. |
| 2 | Press Escape or click outside the second dropdown to dismiss without selecting a tool. | Mention /Ado_repo_M inserted into the Instructions field, highlighted in bold blue. |

## Expected Final State

Mention /Ado_repo_M inserted into the Instructions field, highlighted in bold blue.

## Pass/Fail Criteria

PASS: /Ado_repo_M inserted; no tool suffix; correctly highlighted
FAIL: Nothing inserted; mention includes unwanted tool suffix; highlight absent
