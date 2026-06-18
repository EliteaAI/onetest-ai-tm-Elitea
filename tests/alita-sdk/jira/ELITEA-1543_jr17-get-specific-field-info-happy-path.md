---
id: ELITEA-1543
title: "JR17 - Get Specific Field Info (Happy Path)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [get_specific_field_info, fields, smoke, jira]
requirements: []
---
# ELITEA-1543: JR17 - Get Specific Field Info (Happy Path)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Verify get_specific_field_info retrieves the value of a specific field (e.g., description, priority, assignee) from an existing JIRA issue.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_ISSUE_KEY env var set to an existing issue with known field values
Target field name is a valid JIRA field

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_ISSUE_KEY: key of existing issue with known field values
Field name: priority

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `get_specific_field_info` with JIRA_ISSUE_KEY and a valid field name (e.g., 'priority') | Tool accepts the issue key and field name |
| 3 | Capture the tool response | Response contains the value of the requested field for the specified issue |
| 4 | Validate that the LLM confirms the field value is returned and matches expected content | LLM confirms field value returned without error |

## Expected Final State

LLM confirms field value returned without error

## Pass/Fail Criteria

get_specific_field_info returns field value without error
Returned value is non-empty for a populated field
No exception raised
