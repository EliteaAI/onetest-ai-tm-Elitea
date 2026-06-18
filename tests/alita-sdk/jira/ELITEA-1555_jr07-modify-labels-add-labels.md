---
id: ELITEA-1555
title: "JR07 - Modify Labels (Add Labels)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [modify_labels, labels, jira]
requirements: []
---
# ELITEA-1555: JR07 - Modify Labels (Add Labels)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Verify modify_labels can add one or more labels to an existing JIRA issue, confirming the labels appear on the issue after the operation.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_ISSUE_KEY env var set to an existing issue
Write access to the issue

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_ISSUE_KEY: key of existing issue without the target label
Label to add: automated-test-label
Operation: add

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `modify_labels` with JIRA_ISSUE_KEY and an add operation for a new label not already on the issue (e.g., 'automated-test-label') | Tool accepts the parameters and begins execution |
| 3 | Capture the tool response | Response confirms labels were modified successfully |
| 4 | Validate that the LLM confirms the label was added to the issue | LLM confirms label addition success |

## Expected Final State

LLM confirms label addition success

## Pass/Fail Criteria

modify_labels completes without error
Label appears on the issue after operation
No exception raised
