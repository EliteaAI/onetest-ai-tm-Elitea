---
id: ELITEA-1145
title: "get_pull_request tool handles PR with empty description gracefully"
priority: critical
type: functional
module: ado-toolkit
status: ready
execution_type: manual
tags: [int:ado-repos, feat:toolkits, eng:backend, issue:4497, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4497]
---
# ELITEA-1145: get_pull_request tool handles PR with empty description gracefully

**Module:** Ado Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the get_pull_request tool handles PRs with empty or missing descriptions gracefully without errors.

**Coverage:**
- Tool executes successfully when PR has no description
- Description field returns appropriate value (empty string or null)
- Tool response structure remains valid
- No errors or exceptions thrown

## Preconditions

- User authenticated with valid ADO credentials
- ADO Toolkit configured and connected to target ADO repository
- Test ADO repository accessible with at least one PR with empty/null description
- Environment: {{base_url}}

## Test Data

- ADO Repository: [Test repo with PRs]
- PR ID: [PR with empty description - e.g., PR #456]
- Expected description value: "" or null
- Tool name: get_pull_request

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits from sidebar | Toolkits page loads |
| 2 | Open configured ADO Toolkit in Test Settings | Test Settings panel opens |
| 3 | Select get_pull_request tool from available tools list | Tool is selected |
| 4 | Enter PR ID [e.g., 456] that has no description | PR ID is entered |
| 5 | Execute the tool | Tool execution starts |
| 6 | Review the response JSON/object returned by the tool | Response is displayed |
| 7 | Verify description field is present in the response | Description field exists |
| 8 | Verify description field value is empty string ("") or null | Value is empty or null |
| 9 | Verify tool completes without errors | No errors occur |
| 10 | Verify response structure is valid despite empty description | Structure is valid |

## Expected Final State

Structure is valid

## Pass/Fail Criteria

**Pass:**
- Tool executes without errors
- Response includes description field
- Description field contains empty string or null (documented behavior)
- Response structure is valid
- No exceptions or error messages

**Fail:**
- Tool execution fails with error
- Description field is missing from response
- Tool throws exception when description is empty
- Response structure is invalid
- Error message appears
