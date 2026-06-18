---
id: ELITEA-1551
title: "JR08 - Modify Labels (Remove Labels)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [modify_labels, labels, jira]
requirements: []
---
# ELITEA-1551: JR08 - Modify Labels (Remove Labels)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Verify modify_labels can remove existing labels from a JIRA issue, confirming the labels are no longer present after the operation.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_ISSUE_KEY env var set to an existing issue that already has the target label
Write access to the issue

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_ISSUE_KEY: key of existing issue that already has the target label
Label to remove: automated-test-label
Operation: remove

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `modify_labels` with JIRA_ISSUE_KEY and a remove operation for a label that currently exists on the issue | Tool accepts the parameters and begins execution |
| 3 | Capture the tool response | Response confirms labels were modified successfully |
| 4 | Validate that the LLM confirms the label was removed from the issue | LLM confirms label removal success |

## Expected Final State

LLM confirms label removal success

## Pass/Fail Criteria

modify_labels completes without error
Label removed from the issue after operation
No exception raised
