---
id: ELITEA-2803
title: "Repeating delete_project_context on an already-deleted context is idempotent"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, tool:delete_project_context, idempotency]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2803: Repeating delete_project_context on an already-deleted context is idempotent

## Preconditions

- Test project (project_id 13) is accessible

## Test Data

| Field | Value |
|-------|-------|
| Request payload | `{"project_id": 13}` (called twice in sequence) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call delete_project_context with `{"project_id": 13}` | Context is deleted |
| 2 | Call delete_project_context again with the same payload | No destructive error occurs; the call is a graceful no-op or returns an informative message |

## Expected Final State

A repeated delete on an already-deleted context never throws a destructive/unhandled error.

## Pass/Fail Criteria

**Pass:**
- Second call is a graceful no-op or returns a clear informative message

**Fail:**
- Second call throws an unhandled or destructive error
