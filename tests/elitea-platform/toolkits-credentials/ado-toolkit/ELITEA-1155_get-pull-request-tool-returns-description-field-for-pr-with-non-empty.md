---
id: ELITEA-1155
title: "get_pull_request tool returns description field for PR with non-empty description"
priority: critical
type: functional
module: ado-toolkit
status: ready
execution_type: manual
tags: [int:ado-repos, feat:toolkits, eng:backend, issue:4497, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4497]
---
# ELITEA-1155: get_pull_request tool returns description field for PR with non-empty description

**Module:** Ado Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the get_pull_request tool successfully retrieves and returns the PR description field when the PR has a non-empty description.

**Coverage:**
- Tool executes successfully with description field in response
- Description field contains complete text content from PR
- Existing response fields remain intact (title, status, creator, reviewers, etc.)
- Response structure is valid and properly formatted

## Preconditions

- User authenticated with valid ADO credentials
- ADO Toolkit configured and connected to target ADO repository
- Test ADO repository accessible with at least one PR containing a non-empty description
- Environment: {{base_url}}

## Test Data

- ADO Repository: [Test repo with PRs]
- PR ID: [PR with non-empty description - e.g., PR EliteaAI/elitea_issues#123]
- Expected description content: [Known PR description text]
- Tool name: get_pull_request

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits from sidebar | Toolkits page loads |
| 2 | Open configured ADO Toolkit in Test Settings | Test Settings panel opens |
| 3 | Select get_pull_request tool from available tools list | Tool is selected |
| 4 | Enter PR ID [e.g., 123] that has a non-empty description | PR ID is entered |
| 5 | Execute the tool | Tool execution starts |
| 6 | Review the response JSON/object returned by the tool | Response is displayed |
| 7 | Verify description field is present in the response | Description field exists |
| 8 | Verify description field contains the expected text content | Description matches PR content |
| 9 | Verify all existing fields (title, status, creator, reviewers, etc.) are present | All fields present |
| 10 | Compare response structure with pre-enhancement version (if available) | Structure is valid |

## Expected Final State

Structure is valid

## Pass/Fail Criteria

**Pass:**
- Tool executes without errors
- Response includes description field
- Description field contains complete PR description text
- All existing response fields remain intact
- Response structure is valid JSON/object

**Fail:**
- Tool execution fails with error
- Description field is missing from response
- Description field is empty when PR has content
- Existing fields are missing or corrupted
- Response structure is invalid
