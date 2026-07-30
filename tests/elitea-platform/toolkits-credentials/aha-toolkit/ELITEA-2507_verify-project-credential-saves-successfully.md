---
id: ELITEA-2507
title: "Verify project credential saves successfully"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-2507: Verify project credential saves successfully

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify project-level credential saves successfully with valid data

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application
- User is working within a project context

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open New Aha! Credential form (project scope) | All fields are populated |
| 2 | Enter Display Name: "Test Project Credential" | Success message displays |
| 3 | Verify ID is auto-filled | Credential is saved |
| 4 | Enter Base URL: https://project-test.aha.io | Step completes successfully |
| 5 | Enter valid API Key | Step completes successfully |
| 6 | Click Save button | Step completes successfully |
| 7 | Observe save operation result | Step completes successfully |

## Expected Final State

All fields are populated

## Pass/Fail Criteria

**Pass:**
- All fields are populated
- Success message displays
- Credential is saved

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
