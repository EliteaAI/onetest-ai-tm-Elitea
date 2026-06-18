---
id: ELITEA-1550
title: "JR01 - Search Using JQL (Happy Path)"
priority: critical
type: functional
module: jira
status: ready
execution_type: automated
tags: [search_using_jql, search, smoke, jira]
requirements: []
---
# ELITEA-1550: JR01 - Search Using JQL (Happy Path)

**Module:** Jira · **Priority:** Critical · **Type:** Functional

**Objective:** Verify search_using_jql returns matching issues for a valid JQL query that is expected to produce results.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
Target JIRA project has at least one issue matching the test JQL query

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA_PROJECT_KEY: valid JIRA project key
JQL example: project = ${JIRA_PROJECT_KEY} ORDER BY created DESC

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke the `search_using_jql` tool with a valid JQL query that matches at least one issue (e.g., `project = ${JIRA_PROJECT_KEY} ORDER BY created DESC`) | Tool accepts the JQL query and begins execution |
| 3 | Capture the tool response | Response contains a list of matching issues with key, summary, and status fields |
| 4 | Validate that the LLM confirms the result contains at least one issue with expected structure | LLM confirms results present and well-formed |

## Expected Final State

LLM confirms results present and well-formed

## Pass/Fail Criteria

search_using_jql returns non-empty issues list
Each issue has key, summary, and status
No exception raised
