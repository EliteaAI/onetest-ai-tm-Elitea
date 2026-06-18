---
id: ELITEA-1048
title: "Split Button Dropdown Opens Entity-Type List and Navigates Correctly (Expanded Sidebar)"
priority: critical
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1048: Split Button Dropdown Opens Entity-Type List and Navigates Correctly (Expanded Sidebar)

**Module:** Create Button Redesign · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking the `v` (chevron) part of the split button opens a dropdown listing all available entity types, and selecting each one navigates to the correct creation form.

**Coverage:**
- Dropdown opens on `v` click
- All entity types are listed
- Each selection navigates to the correct form

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Sidebar in expanded state
- On any main section page (e.g., Agents)

## Test Data

Expected dropdown items: Conversation, Agent, Pipeline, Credential, Toolkit, MCP, Artifact Bucket, Integration, Secret, Token, User Invite

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents; click the `v` arrow part of the split button | Dropdown opens listing all entity types |
| 2 | Verify all expected entity type options appear in the dropdown | All listed types are visible: Conversation, Agent, Pipeline, Credential, Toolkit, MCP, Artifact Bucket, Integration, Secret, Token, User Invite |
| 3 | Select `Agent` from the dropdown | New Agent creation form opens; dropdown closes |
| 4 | Reopen the dropdown; select `Pipeline` | New Pipeline creation form opens |
| 5 | Reopen the dropdown; select `Conversation` | New conversation is initiated |
| 6 | Reopen the dropdown; select `Token` | Personal Token creation form opens |
| 7 | Reopen the dropdown; select `Secret` | Secret creation form opens |
| 8 | Reopen the dropdown; select `Invite User` | User invite form opens |

## Expected Final State

User invite form opens

## Pass/Fail Criteria

**Pass:**
- Dropdown opens on `v` click; all entity types are present
- Each selection navigates to the correct creation destination

**Fail:**
- Dropdown does not open
- Any entity type is missing from the list
- A selection navigates to the wrong form or nothing happens
