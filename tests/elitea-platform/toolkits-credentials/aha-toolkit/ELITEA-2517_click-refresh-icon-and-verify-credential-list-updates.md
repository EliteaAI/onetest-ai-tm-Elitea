---
id: ELITEA-2517
title: "Click refresh icon and verify credential list updates"
priority: critical
type: functional
module: toolkits
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2517: Click refresh icon and verify credential list updates

**Module:** Toolkits · **Priority:** Critical · **Type:** Functional

**Objective:** Verify "Refresh the configurations" icon updates credential list dynamically

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User is on Aha! Toolkit configuration page with Aha Configuration dropdown open

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Aha Configuration dropdown | Refresh icon is visible and clickable |
| 2 | Note existing credentials in list | Credential list updates to show newly created credential |
| 3 | Open new browser tab and create new Aha! credential | No page reload required |
| 4 | Return to toolkit configuration tab | Step completes successfully |
| 5 | Click "Refresh the configurations" icon | Step completes successfully |
| 6 | Observe credential list | Step completes successfully |

## Expected Final State

Refresh icon is visible and clickable

## Pass/Fail Criteria

**Pass:**
- Refresh icon is visible and clickable
- Credential list updates to show newly created credential
- No page reload required

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
