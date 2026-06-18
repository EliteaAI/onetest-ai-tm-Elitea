---
id: ELITEA-1532
title: "JR22 - Get Comments with Image Descriptions (No Comments)"
priority: medium
type: functional
module: jira
status: ready
execution_type: automated
tags: [get_comments_with_image_descriptions, edge-case, comments, jira]
requirements: []
---
# ELITEA-1532: JR22 - Get Comments with Image Descriptions (No Comments)

**Module:** Jira · **Priority:** Medium · **Type:** Functional

**Objective:** Test get_comments_with_image_descriptions behavior when the specified issue has no comments, verifying an empty result is returned gracefully.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_ISSUE_KEY_NO_COMMENTS env var set to an existing issue with zero comments

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA issue key: key of existing issue with zero comments

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `get_comments_with_image_descriptions` with a JIRA issue key for an issue with zero comments | Tool accepts the parameters and begins execution |
| 3 | Capture the tool response | Response contains an empty comments list with no error |
| 4 | Validate that the LLM confirms empty result returned gracefully without exception | LLM confirms zero comments returned and no error raised |

## Expected Final State

LLM confirms zero comments returned and no error raised

## Pass/Fail Criteria

get_comments_with_image_descriptions returns empty list for issue with no comments
Tool exits cleanly
