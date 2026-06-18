---
id: ELITEA-1540
title: "JR18 - Get Specific Field Info (Invalid Field)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [get_specific_field_info, error-handling, negative, fields, jira]
requirements: []
---
# ELITEA-1540: JR18 - Get Specific Field Info (Invalid Field)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Test get_specific_field_info behavior when a non-existent or invalid field name is provided, verifying graceful error or empty response.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_ISSUE_KEY env var set to an existing issue
NEGATIVE test — field name used does not exist (e.g., "nonexistent_field_xyz")

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_ISSUE_KEY: key of existing issue
Invalid field name: nonexistent_field_xyz

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `get_specific_field_info` with JIRA_ISSUE_KEY and a non-existent field name (e.g., 'nonexistent_field_xyz') | Tool attempts execution with the invalid field name |
| 3 | Capture the tool response | Error or empty value returned indicating field not found |
| 4 | Validate that the LLM confirms a graceful error or null was returned | LLM confirms error returned without unhandled exception |

## Expected Final State

LLM confirms error returned without unhandled exception

## Pass/Fail Criteria

Tool returns error or null for invalid field name
Tool exits cleanly without stack trace
