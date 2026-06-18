---
id: ELITEA-1545
title: "JR14 - List Projects (Verify Response Structure)"
priority: medium
type: functional
module: jira
status: ready
execution_type: automated
tags: [schema-validation, list_projects, projects, jira]
requirements: []
---
# ELITEA-1545: JR14 - List Projects (Verify Response Structure)

**Module:** Jira · **Priority:** Medium · **Type:** Functional

**Objective:** Verify list_projects response structure includes all expected fields per project object (key, name, projectTypeKey, style, etc.).

## Preconditions

JIRA toolkit is configured and authenticated
JIRA_TOOLKIT_NAME env var is set
User has access to at least one JIRA project

## Test Data

JIRA_TOOLKIT_NAME: name of configured JIRA toolkit
Expected project fields: id, key, name, projectTypeKey, self

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the JIRA toolkit using JIRA_TOOLKIT_NAME env var and valid credentials | Toolkit initializes and connects without error |
| 2 | Invoke `list_projects` and capture the full response | Tool returns the complete projects list |
| 3 | Validate each project object in the response has all expected fields: key, name, id, projectTypeKey, and self URL | Response schema is complete with all expected fields per project |
| 4 | Validate that the LLM confirms the response structure matches the expected JIRA project schema | LLM confirms all required schema fields present in response |

## Expected Final State

LLM confirms all required schema fields present in response

## Pass/Fail Criteria

list_projects returns complete project objects
Each project has id, key, name, and projectTypeKey
No exception raised
