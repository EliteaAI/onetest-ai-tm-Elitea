---
id: ELITEA-1205
title: "TC-012: Jira Toolkit Functional Regression — Tool Call Succeeds After UI Reorganization"
priority: high
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, issue:4029, int:jira, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1205: TC-012: Jira Toolkit Functional Regression — Tool Call Succeeds After UI Reorganization

**Module:** Jira Toolkit Configuration · **Priority:** High · **Type:** Functional

**Objective:** Regression test — verify that after the UI reorganization, a Jira toolkit created through the new form can successfully execute a tool call (e.g., list issues, get issue) and return a valid Jira API response. The UI change should not affect backend functionality.

Coverage:
- New-form toolkit authenticates and connects to Jira
- A tool call (e.g., List Issues) returns a valid response, not an error

## Preconditions

- Logged in as User A with access to a real or sandbox Jira instance
- Valid Jira credentials available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Jira toolkit creation form and fill all required fields using the new reorganized layout | All 8 visible fields present and accept input |
| 2 | Save the toolkit | Toolkit saved; no errors displayed |
| 3 | Open the toolkit's Test Settings / tool invocation panel | Panel opens and shows available Jira tools |
| 4 | Select a read tool (e.g., 'List Issues' or 'Get Issue') and invoke it with minimal valid parameters | Tool call executes without error |
| 5 | Observe the response | Valid Jira API response returned (issue data, project data, etc.) — not an authentication error or 500 |

## Expected Final State

Valid Jira API response returned (issue data, project data, etc.) — not an authentication error or 500

## Pass/Fail Criteria

PASS:
- Tool call executed from Test Settings returns a valid Jira API response (non-error)
- No authentication errors, no 500 errors

FAIL:
- Tool call returns an authentication error or 500
- Toolkit cannot be saved at all
- Connection test fails when it should succeed
