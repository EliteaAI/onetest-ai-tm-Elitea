---
id: ELITEA-1558
title: "JR09 - List Comments (Happy Path)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [list_comments, comments, smoke, jira]
requirements: []
---
# ELITEA-1558: JR09 - List Comments (Happy Path)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Verify list_comments retrieves all comments for an existing JIRA issue that has at least one comment, returning comment body and author data.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_ISSUE_KEY env var set to an issue with at least one comment

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_ISSUE_KEY: key of existing issue with at least one comment

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `list_comments` with JIRA_ISSUE_KEY for an issue that has at least one comment | Tool accepts the issue key and begins execution |
| 3 | Capture the tool response | Response contains a list of comments with author, body, and creation date |
| 4 | Validate that the LLM confirms comments are returned with expected structure | LLM confirms at least one comment returned with author and body fields |

## Expected Final State

LLM confirms at least one comment returned with author and body fields

## Pass/Fail Criteria

list_comments returns non-empty list
Each comment has author and body
No exception raised
