---
id: ELITEA-1552
title: "JR02 - Search Using JQL (No Results)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [search_using_jql, edge-case, search, jira]
requirements: []
---
# ELITEA-1552: JR02 - Search Using JQL (No Results)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Verify search_using_jql handles a valid JQL query that returns no results gracefully, returning an empty list rather than an error.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
JQL query designed to match zero issues (e.g., non-existent label or future date)

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JQL that matches no issues: issue = FAKE-99999999

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `search_using_jql` with a valid JQL query guaranteed to match zero issues (e.g., `issue = FAKE-99999999`) | Tool accepts the query and executes successfully |
| 3 | Capture the tool response | Response contains an empty issues list or zero total count |
| 4 | Validate that the LLM confirms no issues were returned and the result is handled gracefully | LLM confirms empty result returned without error |

## Expected Final State

LLM confirms empty result returned without error

## Pass/Fail Criteria

search_using_jql returns empty list for valid JQL with no matches
No exception raised
Tool handles zero results gracefully
