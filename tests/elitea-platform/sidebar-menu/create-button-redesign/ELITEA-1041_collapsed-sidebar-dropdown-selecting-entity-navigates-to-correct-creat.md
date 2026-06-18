---
id: ELITEA-1041
title: "Collapsed Sidebar Dropdown: Selecting Entity Navigates to Correct Creation Form"
priority: critical
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1041: Collapsed Sidebar Dropdown: Selecting Entity Navigates to Correct Creation Form

**Module:** Create Button Redesign · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that selecting any entity type from the collapsed sidebar dropdown navigates the user to the correct creation form.

**Coverage:**
- Agent, Pipeline, Conversation, Token, Secret, Invite User selections from collapsed dropdown

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Sidebar in collapsed state

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click `+` to open the dropdown; select `Agent` | New Agent creation form opens; dropdown closes |
| 2 | Collapse sidebar; click `+`; select `Pipeline` | New Pipeline creation form opens |
| 3 | Collapse sidebar; click `+`; select `Conversation` | New chat conversation is initiated |
| 4 | Collapse sidebar; click `+`; select `Token` | Personal Token creation form opens |
| 5 | Collapse sidebar; click `+`; select `Secret` | Secret creation form opens |
| 6 | Collapse sidebar; click `+`; select `Invite User` | User invite form opens |

## Expected Final State

User invite form opens

## Pass/Fail Criteria

**Pass:**
- Each selection from collapsed dropdown opens the correct creation destination

**Fail:**
- Selection opens wrong form or navigates to wrong page
- Dropdown remains open after selection
- Nothing happens on selection
