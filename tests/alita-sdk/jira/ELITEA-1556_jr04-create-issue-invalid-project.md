---
id: ELITEA-1556
title: "JR04 - Create Issue (Invalid Project)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [error-handling, create_issue, negative, issues, jira]
requirements: []
---
# ELITEA-1556: JR04 - Create Issue (Invalid Project)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Test create_issue error handling when an invalid or non-existent project key is provided, verifying a descriptive error is returned.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
NEGATIVE test — project key used does not exist in the JIRA instance

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
Invalid project key: INVALID_PROJ_XYZ
Issue type: Task
Summary: Should not be created

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `create_issue` with an invalid project key (e.g., 'INVALID_PROJ_XYZ'), issue type 'Task', and a summary | Tool accepts parameters and attempts execution |
| 3 | Capture the tool response | Error response returned indicating the project key does not exist |
| 4 | Validate that the LLM confirms an appropriate error was returned and no issue was created | LLM confirms error message contains information about the invalid project |

## Expected Final State

LLM confirms error message contains information about the invalid project

## Pass/Fail Criteria

create_issue returns an error for invalid project key
Error message indicates project not found or invalid
No issue created
Tool exits cleanly
