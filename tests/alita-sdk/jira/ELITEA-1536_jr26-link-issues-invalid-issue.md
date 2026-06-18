---
id: ELITEA-1536
title: "JR26 - Link Issues (Invalid Issue)"
priority: medium
type: functional
module: jira
status: ready
execution_type: automated
tags: [error-handling, link_issues, negative, links, jira]
requirements: []
---
# ELITEA-1536: JR26 - Link Issues (Invalid Issue)

**Module:** Jira · **Priority:** Medium · **Type:** Functional

**Objective:** Test link_issues error handling when one or both issue keys are invalid or the link type does not exist, verifying a descriptive error is returned.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
NEGATIVE test — one or both issue keys are non-existent or link type is invalid

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
Non-existent source issue key: FAKE-999999
Link type: blocks

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `link_issues` with a non-existent source issue key (e.g., 'FAKE-999999'), any target key, and any link type | Tool attempts execution with invalid parameters |
| 3 | Capture the tool response | Error returned indicating invalid issue key or link type |
| 4 | Validate that the LLM confirms an error was returned and no link was created | LLM confirms descriptive error message and no link created |

## Expected Final State

LLM confirms descriptive error message and no link created

## Pass/Fail Criteria

link_issues returns error for invalid issue key or link type
Tool exits cleanly
