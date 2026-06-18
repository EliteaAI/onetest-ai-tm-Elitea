---
id: ELITEA-1538
title: "JR16 - Set Issue Status (Invalid Status)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [set_issue_status, error-handling, negative, status, jira]
requirements: []
---
# ELITEA-1538: JR16 - Set Issue Status (Invalid Status)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Test set_issue_status error handling when an invalid or unavailable status name is provided, verifying a descriptive error is returned.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_ISSUE_KEY env var set to an existing issue
NEGATIVE test — status name used is not a valid transition (e.g., "INVALID_STATUS_XYZ")

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_ISSUE_KEY: key of existing issue
Invalid status: INVALID_STATUS_XYZ

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `set_issue_status` with JIRA_ISSUE_KEY and an invalid status name (e.g., 'INVALID_STATUS_XYZ') | Tool attempts execution with the invalid status |
| 3 | Capture the tool response | Error returned indicating the transition is not available |
| 4 | Validate that the LLM confirms an error was returned and the issue status was not changed | LLM confirms error message about invalid transition |

## Expected Final State

LLM confirms error message about invalid transition

## Pass/Fail Criteria

set_issue_status returns error for invalid status name
Error indicates transition not available
Issue status unchanged
Tool exits cleanly
