---
id: ELITEA-1533
title: "JR24 - Get Remote Links (Non-existent Issue)"
priority: medium
type: functional
module: jira
status: ready
execution_type: automated
tags: [get_remote_links, error-handling, negative, links, jira]
requirements: []
---
# ELITEA-1533: JR24 - Get Remote Links (Non-existent Issue)

**Module:** Jira · **Priority:** Medium · **Type:** Functional

**Objective:** Test get_remote_links error handling when a non-existent issue key is provided, verifying a graceful error response.

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
| 2 | Invoke `get_remote_links` with a non-existent issue key (e.g., 'FAKE-999999') | Tool attempts execution with the invalid key |
| 3 | Capture the tool response | Error returned indicating the issue does not exist |
| 4 | Validate that the LLM confirms an error was returned and no links were retrieved | LLM confirms descriptive error message returned |

## Expected Final State

LLM confirms descriptive error message returned

## Pass/Fail Criteria

get_remote_links returns error for non-existent issue
Tool exits cleanly
