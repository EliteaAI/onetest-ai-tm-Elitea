---
id: ELITEA-2807
title: "generate_project_context_draft enforces the documented 2500-character limit on user_description"
priority: medium
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, tool:generate_project_context_draft, boundary]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2807: generate_project_context_draft enforces the documented 2500-character limit on user_description

## Preconditions

- Test project (project_id 13) is accessible

## Test Data

| Field | Value |
|-------|-------|
| Request payload | `{"project_id": 13, "user_description": "<text intentionally exceeding 2500 characters>"}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call generate_project_context_draft with a user_description exceeding 2500 characters | The input is truncated or explicitly rejected per the documented limit; no unhandled crash occurs |

## Expected Final State

The documented 2500-character limit on user_description is consistently enforced.

## Pass/Fail Criteria

**Pass:**
- Limit enforced consistently via truncation or a clear rejection

**Fail:**
- Limit is ignored and the oversized input is silently accepted and processed, or the call crashes unhandled
