---
id: ELITEA-2805
title: "generate_project_context_draft produces a valid markdown draft in create mode with a default model"
priority: high
type: functional
module: project-context
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, tool:generate_project_context_draft]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-2805: generate_project_context_draft produces a valid markdown draft in create mode with a default model

## Preconditions

- Test project (project_id 13) is accessible

## Test Data

| Field | Value |
|-------|-------|
| Request payload | `{"project_id": 13, "user_description": "QA test project background for a Python API service."}` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Call generate_project_context_draft with a project_id and user_description, without current_project_background | A valid, well-formed markdown draft is returned that is relevant to the description |

## Expected Final State

A create-mode draft request produces a valid, relevant markdown project context draft.

## Pass/Fail Criteria

**Pass:**
- Valid markdown draft returned, relevant to the description

**Fail:**
- Empty response, malformed markdown, or content unrelated to the description
