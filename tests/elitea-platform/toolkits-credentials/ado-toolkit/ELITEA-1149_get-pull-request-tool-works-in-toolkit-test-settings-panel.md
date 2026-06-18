---
id: ELITEA-1149
title: "get_pull_request tool works in Toolkit Test Settings panel"
priority: high
type: functional
module: ado-toolkit
status: ready
execution_type: manual
tags: [int:ado-repos, feat:toolkits, eng:backend, issue:4497, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4497]
---
# ELITEA-1149: get_pull_request tool works in Toolkit Test Settings panel

**Module:** Ado Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify that get_pull_request tool can be tested directly in the Toolkit Test Settings panel and returns description field correctly.

**Coverage:**
- Tool can be executed from Toolkit Test Settings
- Description field appears in test execution results
- Tool response is properly formatted and readable
- Test Settings UI displays description content correctly

## Preconditions

- User authenticated with valid ADO credentials
- ADO Toolkit configured and saved
- Test ADO repository accessible with at least one PR
- Environment: {{base_url}}

## Test Data

- Toolkit name: ADO Toolkit
- Tool name: get_pull_request
- PR ID: [Valid PR ID with description]
- Expected fields in response: title, status, creator, reviewers, description

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits from sidebar | Toolkits page loads |
| 2 | Locate configured ADO Toolkit and click on it | Toolkit opens |
| 3 | Click "Test Settings" or equivalent action to open toolkit testing interface | Test Settings opens |
| 4 | In the tools list, select get_pull_request | Tool selected |
| 5 | Enter required parameters (PR ID) | Parameters entered |
| 6 | Click Execute/Run to test the tool | Tool executes |
| 7 | Wait for tool execution to complete | Execution completes |
| 8 | Review the response displayed in Test Settings panel | Response displayed |
| 9 | Verify description field is visible in the response | Description visible |
| 10 | Verify description content is readable and properly formatted | Content readable |
| 11 | Verify response JSON/object is valid and well-structured | Response valid |

## Expected Final State

Response valid

## Pass/Fail Criteria

**Pass:**
- Tool executes successfully in Test Settings
- Response includes description field
- Description content is visible and readable
- Response is properly formatted
- Test Settings UI displays all response fields clearly

**Fail:**
- Tool execution fails in Test Settings
- Description field is missing from response
- Response is not displayed or is unreadable
- UI does not render description content
- Execution errors appear
