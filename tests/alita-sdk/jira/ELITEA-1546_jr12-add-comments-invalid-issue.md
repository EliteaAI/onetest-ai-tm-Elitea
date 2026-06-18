---
id: ELITEA-1546
title: "JR12 - Add Comments (Invalid Issue)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [error-handling, add_comments, negative, comments, jira]
requirements: []
---
# ELITEA-1546: JR12 - Add Comments (Invalid Issue)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Test add_comments error handling when commenting on an invalid or non-existent issue key, verifying a descriptive error is returned.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
NEGATIVE test — issue key used does not exist

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
Non-existent issue key: FAKE-999999
Comment body: Should not be posted

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `add_comments` with a non-existent or invalid issue key (e.g., 'FAKE-999999') and a comment body | Tool attempts execution |
| 3 | Capture the tool response | Error returned indicating issue does not exist |
| 4 | Validate that the LLM confirms an error was returned and no comment was created | LLM confirms error message and no comment ID returned |

## Expected Final State

LLM confirms error message and no comment ID returned

## Pass/Fail Criteria

add_comments returns error for invalid issue key
No comment created
Tool exits cleanly
