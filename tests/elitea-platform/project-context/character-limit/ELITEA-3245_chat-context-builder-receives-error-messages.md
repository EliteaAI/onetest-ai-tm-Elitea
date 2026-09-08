---
id: ELITEA-3245
title: "Chat: Project Context Builder tool receives error messages when limit exceeded"
priority: critical
type: functional
module: project-context
status: draft
execution_type: manual
tags: [feat:project-setup, feat:chat, story:6344, r-2.0.6, project-context-builder, tool:generate_project_context_draft, error-handling]
requirements: [EliteaAI/elitea_issues#6344]
---

# ELITEA-3245: Chat: Project Context Builder tool receives error messages when limit exceeded

## Preconditions

- User has access to Chat with Project Context Builder module enabled
- Project Context Builder toggle is ON in Default Modules (Settings → General)
- Test project is available

## Test Data

| Field | Value |
|-------|-------|
| Chat message | "Create a very detailed and comprehensive project context that covers all aspects of our enterprise software platform including architecture, integrations, security, compliance, deployment, and maintenance procedures" |
| Character limit | 2500 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a new Chat conversation | Chat interface loads |
| 2 | Verify Project Context Builder module is enabled | Module is active in chat |
| 3 | Send a message requesting verbose project context generation | AI processes the request and invokes generate_project_context_draft tool |
| 4 | Observe the tool's internal behavior (via logs or AI thought process) | Tool receives any error messages from the backend |
| 5 | If first attempt exceeds limit, observe retry behavior | Tool should receive error feedback and use it for regeneration |
| 6 | Wait for final output | Final content respects the 2500 char limit |

## Expected Final State

The Chat Project Context Builder internal tool receives and can act upon error messages when generated content exceeds the 2500-character limit.

## Pass/Fail Criteria

**Pass:**
- Tool receives clear error message when limit is exceeded
- Error message enables the tool to understand the issue
- Tool can use error feedback to regenerate compliant content
- Final output is ≤2500 characters

**Fail:**
- Tool does not receive error messages
- Tool retries without awareness of the limit violation
- Tool produces truncated content without error handling
- Multiple retries occur without improvement
