---
id: ELITEA-3979
title: "Partial update omitting content must preserve existing content, not wipe it"
priority: critical
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, tool:put_project_context, data-loss]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3979: Partial update omitting content must preserve existing content, not wipe it

## Preconditions

- Test project (project_id 13) is accessible
- Project 13 has existing non-empty `content`

## Test Data

| Field | Value |
|-------|-------|
| Request payload | `{"project_id": 13, "enabled": true}` (no `content` field) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call get_project_context and note the existing content | Non-empty content is returned |
| 2 | Call put_project_context with only `{"project_id": 13, "enabled": true}` | Only `enabled` is intended to update; `content` is expected to remain unaffected |
| 3 | Call get_project_context again and compare | Content is expected to be identical to the value noted in step 1; `enabled` is true |

## Expected Final State

Omitting `content` from an update must never remove or reset existing content — only the fields explicitly provided should change.

## Pass/Fail Criteria

**Pass:**
- Existing content preserved verbatim; only `enabled` changes

**Fail:**
- Content is wiped, reset, or otherwise altered by an update payload that did not include it
