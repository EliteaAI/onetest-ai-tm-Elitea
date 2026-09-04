---
id: ELITEA-3238
title: "Updating Project Context Applies to New Messages in Chat"
priority: critical
type: functional
module: project-context
status: draft
execution_type: manual
tags: [project-context, chat, r-2.0.6, eng:optimization]
requirements: [EliteaAI/elitea_issues#5326]
---

## Preconditions

- User is logged in to `{{base_url}}`
- 
- Initial Project Context: `Version A: Project is in planning phase`

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Initial Context | `Version A: Project is in planning phase` |
| Updated Context | `Version B: Project is now in development phase` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Set Project Context to "Version A: Project is in planning phase" | Context saved |
| 1 | Start new chat, ask: "What phase is the project in?" | Chat responds: "planning phase" |
| 2 | Update Project Context to "Version B: Project is now in development phase" | Context updated and saved |
| 3 | In the **same chat**, send new message: "What phase is the project in now?" | Chat responds: "development phase" (updated context applied) |
| 4 | Start a **new chat**, ask: "What phase is the project in?" | New chat also uses updated context: "development phase" |

## Expected Final State

Updated Project Context applies to new messages in existing chat and to new chats. Optimization doesn't break context update mechanism.

## Pass/Fail Criteria

**Pass:**
- Initial context applied correctly
- Updated context applied to new messages in same chat
- Updated context applied to new chats
- No stale context served

**Fail:**
- Updated context not applied
- Stale context served after update
- Context update doesn't propagate
- Errors after context update
