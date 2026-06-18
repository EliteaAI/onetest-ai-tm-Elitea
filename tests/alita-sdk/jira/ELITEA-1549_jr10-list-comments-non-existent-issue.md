---
id: ELITEA-1549
title: "JR10 - List Comments (Non-existent Issue)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [error-handling, list_comments, negative, comments, jira]
requirements: []
---
# ELITEA-1549: JR10 - List Comments (Non-existent Issue)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Test list_comments error handling when the specified issue key does not exist, verifying a graceful error response.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
NEGATIVE test — issue key used does not exist

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
Non-existent issue key: FAKE-999999

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `list_comments` with a non-existent issue key (e.g., 'FAKE-999999') | Tool attempts execution with the invalid key |
| 3 | Capture the tool response | Error returned indicating issue does not exist |
| 4 | Validate that the LLM confirms an error was returned and no comments were listed | LLM confirms error message is descriptive |

## Expected Final State

LLM confirms error message is descriptive

## Pass/Fail Criteria

list_comments returns error for non-existent issue
Tool exits cleanly
No unhandled exception
