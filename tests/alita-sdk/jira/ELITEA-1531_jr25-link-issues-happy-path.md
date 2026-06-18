---
id: ELITEA-1531
title: "JR25 - Link Issues (Happy Path)"
priority: medium
type: functional
module: jira
status: ready
execution_type: automated
tags: [link_issues, links, jira]
requirements: []
---
# ELITEA-1531: JR25 - Link Issues (Happy Path)

**Module:** Jira · **Priority:** Medium · **Type:** Functional

**Objective:** Verify link_issues creates an issue link between two valid JIRA issues with a specified link type (e.g., "blocks", "relates to").

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JIRA_ISSUE_KEY and JIRA_LINKED_ISSUE_KEY env vars set to two valid issue keys
Write access to both issues
Link type is valid for the JIRA instance

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_ISSUE_KEY: source issue key with write access
JIRA_LINKED_ISSUE_KEY: target issue key
Link type: relates to

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `link_issues` with two valid issue keys (JIRA_ISSUE_KEY and JIRA_LINKED_ISSUE_KEY) and a valid link type (e.g., 'relates to') | Tool accepts all parameters and begins execution |
| 3 | Capture the tool response | Response confirms the link was created between the two issues |
| 4 | Validate that the LLM confirms the link was successfully created with the correct type | LLM confirms link creation success and correct link type |

## Expected Final State

LLM confirms link creation success and correct link type

## Pass/Fail Criteria

link_issues completes without error
Link type and target issue reflected on source issue
No exception raised
