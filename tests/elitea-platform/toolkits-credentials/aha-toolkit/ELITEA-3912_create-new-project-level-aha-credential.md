---
id: ELITEA-3912
title: "Create new project-level Aha! credential"
priority: critical
type: functional
module: credentials
status: ready
execution_type: manual
tags: [feat:aha-toolkit, module:toolkits-credentials, priority:p0]
requirements: [EliteaAI/elitea_issues#5907]
---
# ELITEA-3912: Create new project-level Aha! credential

**Module:** Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify user can successfully create a new project-level Aha! credential

**Coverage:**
- AC from Story #5907: Aha! toolkit integration testing

## Preconditions

- User logged in to Elitea application
- User has valid Aha! API credentials
- User is working within a project context

## Test Data

- Test environment: https://dev.elitea.ai/ or https://next.elitea.ai/

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Credentials page or Aha Configuration dropdown | Project-level credential form opens |
| 2 | Click "New project aha credentials" option | All fields accept input |
| 3 | Enter Display Name: "Project Shared Credential" | Credential saves successfully |
| 4 | Verify ID field is auto-filled | Step completes successfully |
| 5 | Enter Base URL: https://project-subdomain.aha.io | Step completes successfully |
| 6 | Enter valid API Key | Step completes successfully |
| 7 | Click Save button | Step completes successfully |

## Expected Final State

Project-level credential form opens

## Pass/Fail Criteria

**Pass:**
- Project-level credential form opens
- All fields accept input
- Credential saves successfully

**Fail:**
- Any expected result is not achieved
- Errors occur during test execution
