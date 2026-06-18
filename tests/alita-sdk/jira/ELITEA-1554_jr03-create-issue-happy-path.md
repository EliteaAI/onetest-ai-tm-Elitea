---
id: ELITEA-1554
title: "JR03 - Create Issue (Happy Path)"
priority: critical
type: functional
module: jira
status: ready
execution_type: automated
tags: [create_issue, issues, smoke, jira]
requirements: []
---
# ELITEA-1554: JR03 - Create Issue (Happy Path)

**Module:** Jira · **Priority:** Critical · **Type:** Functional

**Objective:** Verify create_issue creates a new JIRA issue in a valid project with required fields, returning the new issue key.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_PROJECT_KEY env var set to an existing project key
Write access to the project

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_PROJECT_KEY: valid project key
Issue type: Task
Summary: Automated test issue

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `create_issue` with valid project key (JIRA_PROJECT_KEY), issue type (e.g., 'Task'), and summary (e.g., 'Automated test issue') | Tool accepts the parameters and begins execution |
| 3 | Capture the tool response | Response includes the newly created issue key (e.g., PROJ-123) |
| 4 | Validate that the LLM confirms the issue was created and returns a valid JIRA issue key | LLM confirms issue key returned in expected format |

## Expected Final State

LLM confirms issue key returned in expected format

## Pass/Fail Criteria

create_issue returns a valid issue key
Issue key matches pattern PROJECT-NUMBER
No exception raised
