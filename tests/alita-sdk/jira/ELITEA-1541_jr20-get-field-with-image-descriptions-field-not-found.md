---
id: ELITEA-1541
title: "JR20 - Get Field with Image Descriptions (Field Not Found)"
priority: medium
type: functional
module: jira
status: ready
execution_type: automated
tags: [get_field_with_image_descriptions, negative, fields, jira]
requirements: []
---
# ELITEA-1541: JR20 - Get Field with Image Descriptions (Field Not Found)

**Module:** Jira · **Priority:** Medium · **Type:** Functional

**Objective:** Test get_field_with_image_descriptions behavior when the requested field does not exist or does not contain images, verifying a graceful response.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_ISSUE_KEY env var set to an existing issue
NEGATIVE test — field name used does not exist on the issue

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_ISSUE_KEY: key of existing issue
Invalid field name: nonexistent_field_xyz

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `get_field_with_image_descriptions` with JIRA_ISSUE_KEY and a non-existent field name (e.g., 'nonexistent_field_xyz') | Tool attempts execution with the invalid field name |
| 3 | Capture the tool response | Error or empty response indicating the field was not found |
| 4 | Validate that the LLM confirms a graceful error was returned | LLM confirms error returned without unhandled exception |

## Expected Final State

LLM confirms error returned without unhandled exception

## Pass/Fail Criteria

Tool returns error or null for field not found
Tool exits cleanly
