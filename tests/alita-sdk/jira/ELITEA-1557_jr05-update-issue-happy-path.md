---
id: ELITEA-1557
title: "JR05 - Update Issue (Happy Path)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [update_issue, issues, smoke, jira]
requirements: []
---
# ELITEA-1557: JR05 - Update Issue (Happy Path)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Verify update_issue modifies fields of an existing JIRA issue (e.g., summary, description, priority) and confirms the changes are applied.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_ISSUE_KEY env var set to an existing issue key
Write access to the issue

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_ISSUE_KEY: key of an existing JIRA issue with write access
Field to update: summary
New value: Updated by automated test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `update_issue` with JIRA_ISSUE_KEY and a valid field update (e.g., new summary or description) | Tool accepts the parameters and begins execution |
| 3 | Capture the tool response | Response confirms the issue was updated successfully |
| 4 | Validate that the LLM confirms the update was applied and the response indicates success | LLM confirms update success and field value changed |

## Expected Final State

LLM confirms update success and field value changed

## Pass/Fail Criteria

update_issue completes without error
Issue fields reflect updated values
No exception raised
