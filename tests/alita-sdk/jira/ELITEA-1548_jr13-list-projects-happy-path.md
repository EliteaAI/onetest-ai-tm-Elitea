---
id: ELITEA-1548
title: "JR13 - List Projects (Happy Path)"
priority: high
type: functional
module: jira
status: ready
execution_type: automated
tags: [list_projects, projects, smoke, jira]
requirements: []
---
# ELITEA-1548: JR13 - List Projects (Happy Path)

**Module:** Jira · **Priority:** High · **Type:** Functional

**Objective:** Verify list_projects returns the list of JIRA projects accessible to the configured user, with project key and name metadata.

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
User has access to at least one JIRA project

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
JIRA user must have access to at least one project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `list_projects` with no special filters | Tool begins execution and queries all accessible projects |
| 3 | Capture the tool response | Response contains a list of JIRA projects each with key and name |
| 4 | Validate that the LLM confirms projects are returned with key and name for each entry | LLM confirms project list includes key and name fields for each project |

## Expected Final State

LLM confirms project list includes key and name fields for each project

## Pass/Fail Criteria

list_projects returns non-empty list
Each project has key and name
No exception raised
