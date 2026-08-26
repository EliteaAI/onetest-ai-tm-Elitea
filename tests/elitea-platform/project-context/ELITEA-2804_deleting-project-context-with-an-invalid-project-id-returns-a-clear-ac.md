---
id: ELITEA-2804
title: "Deleting project context with an invalid project_id returns a clear access-denied error"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, tool:delete_project_context, negative]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2804: Deleting project context with an invalid project_id returns a clear access-denied error

## Preconditions

- An invalid/inaccessible project_id (e.g. 99999) is available for testing

## Test Data

| Field | Value |
|-------|-------|
| Request payload | `{"project_id": 99999}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call delete_project_context with an invalid project_id (99999) | A clear `access_denied` error is returned |

## Expected Final State

A delete against a non-existent or inaccessible project fails with a clear, structured error.

## Pass/Fail Criteria

**Pass:**
- Clear structured error returned

**Fail:**
- Silent failure or a generic unhandled error occurs
