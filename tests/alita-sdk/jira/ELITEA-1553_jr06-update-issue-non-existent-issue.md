---
id: ELITEA-1553
title: "JR06 - Update Issue (Non-existent Issue)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [error-handling, update_issue, negative, issues, jira]
requirements: []
---
# ELITEA-1553: JR06 - Update Issue (Non-existent Issue)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Test update_issue error handling when the specified issue key does not exist, verifying a descriptive error is returned without crashing.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
NEGATIVE test — issue key used does not exist (e.g., INVALID-99999)

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
Non-existent issue key: FAKE-999999
Field: summary
Value: Should not update

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `update_issue` with a non-existent issue key (e.g., 'FAKE-999999') and any valid field update | Tool attempts execution with the non-existent key |
| 3 | Capture the tool response | Error returned indicating the issue does not exist |
| 4 | Validate that the LLM confirms an error was returned and no update was applied | LLM confirms error message is descriptive and no changes were made |

## Expected Final State

LLM confirms error message is descriptive and no changes were made

## Pass/Fail Criteria

update_issue returns error for non-existent issue key
Error message indicates issue not found
Tool exits cleanly
