---
id: ELITEA-1029
title: "Expanded Split Button Dropdown: All Entity Types Present and Selectable"
priority: medium
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1029: Expanded Split Button Dropdown: All Entity Types Present and Selectable

**Module:** Create Button Redesign · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the split button dropdown in expanded mode contains all entity types and each is selectable and navigates correctly.

**Coverage:**
- Dropdown completeness in expanded mode
- All items are clickable and functional

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Sidebar in expanded state

## Test Data

Expected items: Conversation, Agent, Pipeline, Credential, Toolkit, MCP, Artifact Bucket, Integration, Secret, Token, User Invite

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents; click the `v` arrow on the split button | Dropdown opens |
| 2 | Count and verify all entity types: Conversation, Agent, Pipeline, Credential, Toolkit, MCP, Artifact Bucket, Integration, Secret, Token, User Invite | All 11 items visible |
| 3 | Click each item one at a time (reopening dropdown between selections) | Each selection navigates to the correct creation form |

## Expected Final State

Each selection navigates to the correct creation form

## Pass/Fail Criteria

**Pass:**
- All 11 entity types listed; all are clickable and navigate correctly

**Fail:**
- Any item is greyed out, missing, or non-interactive
- Dropdown closes without action on any item click
