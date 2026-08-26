---
id: ELITEA-2802
title: "Clean delete of an existing project context via delete_project_context"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, tool:delete_project_context]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2802: Clean delete of an existing project context via delete_project_context

## Preconditions

- Test project (project_id 13) has an existing project context

## Test Data

| Field | Value |
|-------|-------|
| Request payload | `{"project_id": 13}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call delete_project_context with `{"project_id": 13}` | Context configuration is removed |
| 2 | Call get_project_context | No context content is returned (empty/default state) |

## Expected Final State

An existing project context is fully and cleanly removed by delete_project_context.

## Pass/Fail Criteria

**Pass:**
- Context configuration fully removed

**Fail:**
- Context remains after deletion, or the delete call errors on a valid target
