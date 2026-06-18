---
id: ELITEA-1045
title: "Collapsed Sidebar: Clicking `+` Opens Full Entity-Type Dropdown"
priority: critical
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1045: Collapsed Sidebar: Clicking `+` Opens Full Entity-Type Dropdown

**Module:** Create Button Redesign · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking the `+` button in collapsed sidebar mode opens a dropdown listing all available entity types.

**Coverage:**
- Dropdown visibility on click in collapsed mode
- All entity types present in the dropdown

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Sidebar in collapsed state

## Test Data

Expected dropdown items: Conversation, Agent, Pipeline, Credential, Toolkit, MCP, Artifact Bucket, Integration, Secret, Token, User Invite

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Collapse the sidebar | Sidebar collapses; `+` icon visible |
| 2 | Click the `+` icon | Dropdown opens adjacent to the button |
| 3 | Inspect all items in the dropdown | All expected entity types are listed: Conversation, Agent, Pipeline, Credential, Toolkit, MCP, Artifact Bucket, Integration, Secret, Token, User Invite |
| 4 | Click outside the dropdown | Dropdown closes without navigation |

## Expected Final State

Dropdown closes without navigation

## Pass/Fail Criteria

**Pass:**
- Dropdown opens on `+` click in collapsed mode
- All entity types are present

**Fail:**
- Dropdown does not open
- Any entity type is missing
- Dropdown immediately closes before user can interact
