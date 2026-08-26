---
id: ELITEA-2799
title: "Full update of project context sets both content and enabled via put_project_context"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, tool:put_project_context]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2799: Full update of project context sets both content and enabled via put_project_context

## Preconditions

- Test project (project_id 13) is accessible

## Test Data

| Field | Value |
|-------|-------|
| Request payload | `{"project_id": 13, "content": "<full markdown context>", "enabled": true}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call put_project_context with a full payload (content + enabled=true) | Context is updated with the new content; `enabled` is set to true |
| 2 | Call get_project_context to confirm persisted state | Returned content matches the update; `enabled` is true |

## Expected Final State

A full-payload update persists both content and enabled state correctly.

## Pass/Fail Criteria

**Pass:**
- Content and enabled state both persist exactly as sent

**Fail:**
- Content or enabled state is not persisted, or persisted incorrectly
