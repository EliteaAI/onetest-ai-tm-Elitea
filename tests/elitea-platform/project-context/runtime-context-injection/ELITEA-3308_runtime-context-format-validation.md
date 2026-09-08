---
id: ELITEA-3308
title: "runtime_context format matches expected XML structure with user_id and project_id"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:context-management, feat:toolkits, story:6306, r-2.0.6, runtime-context, format-validation]
requirements: [EliteaAI/elitea_issues#6306]
---

# ELITEA-3308: runtime_context format matches expected XML structure with user_id and project_id

## Preconditions

- User is logged in to `{{base_url}}`
- Access to backend logs or debug mode to inspect runtime_context
- User ID and Project ID are known for validation

## Test Data

| Field | Value |
|-------|-------|
| Expected format | `<runtime_context>\n  <user_id>{{user_id}}</user_id>\n  <project_id>{{project_id}}</project_id>\n</runtime_context>` |
| User ID | (obtain from user profile or API) |
| Project ID | (obtain from project settings or URL) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Enable Skills Builder and Project Context Builder | Both modules enabled |
| 2 | Enable debug/verbose logging or use network inspection to capture tool initialization | Debug mode active |
| 3 | Trigger Project Context Builder by sending a context creation request | Tool is initialized |
| 4 | Inspect the runtime_context passed to the tool | Format matches: `<runtime_context>\n  <user_id>X</user_id>\n  <project_id>Y</project_id>\n</runtime_context>` |
| 5 | Verify user_id value matches the current logged-in user | user_id is correct |
| 6 | Verify project_id value matches the current project | project_id is correct |
| 7 | Repeat for Skill Builder | Same format and correct values observed |

## Expected Final State

The runtime_context injected into Project Context Builder and Skill Builder follows the exact documented format with accurate user_id and project_id values.

## Pass/Fail Criteria

**Pass:**
- runtime_context uses the documented XML format
- user_id matches current user
- project_id matches current project
- Format is consistent across both tools

**Fail:**
- Different format used (JSON, different XML structure, etc.)
- Incorrect user_id or project_id values
- Missing elements in the context
