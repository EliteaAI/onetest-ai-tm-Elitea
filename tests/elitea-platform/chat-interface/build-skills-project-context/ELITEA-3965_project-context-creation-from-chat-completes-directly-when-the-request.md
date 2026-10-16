---
id: ELITEA-3965
title: "Project Context creation from chat completes directly when the request already contains all required information"
priority: high
type: functional
module: chat-interface
status: ready
execution_type: manual
tags: [feat:chat, story:6239, r-2.0.6, project-context-builder, happy-path]
requirements: [EliteaAI/elitea_issues#6239]
---

# ELITEA-3965: Project Context creation from chat completes directly when the request already contains all required information

## Preconditions

- User is logged in to `{{base_url}}`
- Project Context Builder is enabled
- The current project has no existing Project Context configured

## Test Data

| Field | Value |
|-------|-------|
| Context content | "This project is a Python REST API for order management." |
| Scope | All conversations in the project |
| Tags | backend, api |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a chat message providing the context content, scope, and tags in full | The assistant proceeds to create the Project Context without asking clarifying questions |
| 2 | Inspect the created Project Context | Content, scope, and tags match exactly what was provided |
| 3 | Check the chat response | A "Project Context: [context name]" chip/link is shown in the chat response |

## Expected Final State

A fully specified chat request creates a new Project Context with correctly populated fields and a visible chip/link.

## Pass/Fail Criteria

**Pass:**
- Project Context created with correct content/scope/tags
- Project Context chip/link shown in chat response

**Fail:**
- Project Context not created, created with incorrect/missing fields, or an unnecessary clarifying question is shown
