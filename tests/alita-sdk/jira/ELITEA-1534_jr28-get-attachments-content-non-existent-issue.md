---
id: ELITEA-1534
title: "JR28 - Get Attachments Content (Non-existent Issue)"
priority: medium
type: functional
module: jira
status: ready
execution_type: automated
tags: [get_attachments_content, error-handling, attachments, negative, jira]
requirements: []
---
# ELITEA-1534: JR28 - Get Attachments Content (Non-existent Issue)

**Module:** Jira · **Priority:** Medium · **Type:** Functional

**Objective:** Test get_attachments_content error handling when a non-existent issue key is provided, verifying a graceful error response.

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
| 2 | Invoke `get_attachments_content` with a non-existent issue key (e.g., 'FAKE-999999') | Tool attempts execution with invalid key |
| 3 | Capture the tool response | Error returned indicating the issue does not exist |
| 4 | Validate that the LLM confirms an error was returned and no attachment content was retrieved | LLM confirms descriptive error returned without exception |

## Expected Final State

LLM confirms descriptive error returned without exception

## Pass/Fail Criteria

get_attachments_content returns error for non-existent issue
Tool exits cleanly
