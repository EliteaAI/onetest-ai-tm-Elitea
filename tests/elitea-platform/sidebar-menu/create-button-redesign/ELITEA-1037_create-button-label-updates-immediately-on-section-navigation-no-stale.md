---
id: ELITEA-1037
title: "Create Button Label Updates Immediately on Section Navigation (No Stale State)"
priority: high
type: functional
module: create-button-redesign
status: ready
execution_type: manual
tags: [r-2.0.4]
requirements: [EliteaAI/elitea_issues#5135]
---
# ELITEA-1037: Create Button Label Updates Immediately on Section Navigation (No Stale State)

**Module:** Create Button Redesign · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Create button label updates instantly to reflect the new section as the user navigates, without requiring a page refresh.

**Coverage:**
- Label reactivity across sequential navigation
- Stale state after rapid navigation

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Sidebar in expanded state

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents; observe button label | Shows `+ Agent` |
| 2 | Immediately click Pipelines in the sidebar | Button updates to `+ Pipeline` without page reload |
| 3 | Immediately click Credentials | Button updates to `+ Credential` |
| 4 | Rapidly click: Chat → Toolkits → Artifacts → Agents | Button label follows each click in sequence; final label is `+ Agent` |
| 5 | After rapid navigation, click `+ Agent` | New Agent creation form opens correctly |

## Expected Final State

New Agent creation form opens correctly

## Pass/Fail Criteria

**Pass:**
- Label updates immediately on each navigation click
- Final state after rapid navigation is correct
- Creation form opened matches the final label

**Fail:**
- Label is delayed in updating after navigation
- Label shows stale entity name after rapid navigation
- Creation form does not match the displayed label
