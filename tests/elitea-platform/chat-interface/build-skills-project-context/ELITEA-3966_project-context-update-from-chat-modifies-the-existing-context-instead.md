---
id: ELITEA-3966
title: "Project Context update from chat modifies the existing context instead of creating a duplicate"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3966: Project Context update from chat modifies the existing context instead of creating a duplicate

## Preconditions

- User is logged in to `{{base_url}}`
- Project Context Builder is enabled
- An existing Project Context is already configured for the project

## Test Data

| Field | Value |
|-------|-------|
| Update request | "Update the project context to mention we now support GraphQL in addition to REST." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the update request in chat | The assistant updates the existing Project Context rather than creating a new one |
| 2 | Inspect the Project Context afterward | The existing entity now includes the GraphQL detail; no duplicate Project Context entity exists |
| 3 | Check the chat response | A "Project Context: [context name]" chip/link is shown, referencing the updated entity |

## Expected Final State

Requesting an update from chat modifies the single existing Project Context in place.

## Pass/Fail Criteria

**Pass:**
- Existing Project Context updated with new content
- No duplicate Project Context created
- Chip/link shown referencing the updated entity

**Fail:**
- A duplicate Project Context is created instead of updating the existing one
- The update is not applied
