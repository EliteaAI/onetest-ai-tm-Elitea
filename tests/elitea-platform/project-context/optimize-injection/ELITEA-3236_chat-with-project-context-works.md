---
id: ELITEA-3236
title: "Chat with Project Context Works (Existing and New Conversations)"
priority: critical
type: regression
module: project-context
status: draft
execution_type: manual
tags: [project-context, chat, r-2.0.6, eng:optimization]
requirements: [EliteaAI/elitea_issues#5326]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Existing chat conversation exists
- Project Context is enabled and contains test phrase: `QA-CONTEXT-TEST: Chat context verification`

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test Phrase | `QA-CONTEXT-TEST: Chat context verification` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open existing chat conversation | Chat loads without errors |
| 2 | Send message: "What is the QA-CONTEXT-TEST phrase?" | Chat invokes `read_project_context` tool, returns: "Chat context verification" |
| 3 | Verify chat history is intact | All previous messages visible and correct |
| 4 | Click "New Chat" button | New conversation created |
| 5 | In new chat, send message: "What is the QA-CONTEXT-TEST phrase?" | Chat invokes `read_project_context` tool, returns: "Chat context verification" |
| 6 | Ask: "Repeat the phrase" | Chat repeats phrase correctly in both conversations |

## Expected Final State

Both existing and new chat conversations work correctly with Project Context. Context is applied, tool call visible in UI, chat history preserved.

## Pass/Fail Criteria

**Pass:**
- Existing chat loads without errors
- New chat created successfully
- Project Context phrase returned correctly in both chats
- `read_project_context` tool call visible in UI
- Chat history intact in existing conversation

**Fail:**
- Chat fails to load or create
- Context not applied in either chat
- Tool call not visible
- Chat history lost
- Errors in console/logs
