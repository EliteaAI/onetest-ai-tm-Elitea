---
id: ELITEA-3980
title: "Updating project context with an invalid project_id returns a clear access-denied error"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, tool:put_project_context, negative]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3980: Updating project context with an invalid project_id returns a clear access-denied error

## Preconditions

- An invalid/inaccessible project_id (e.g. 99999) is available for testing

## Test Data

| Field | Value |
|-------|-------|
| Request payload | `{"project_id": 99999, "content": "test", "enabled": true}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call put_project_context with an invalid project_id (99999) | A clear `access_denied`/`not_found` error is returned; no data is written |

## Expected Final State

An update against a non-existent or inaccessible project fails with a clear, structured error and no side effects.

## Pass/Fail Criteria

**Pass:**
- Clear, structured error returned; no side effects

**Fail:**
- Silent failure, a generic unhandled error, or a partial write occurs
