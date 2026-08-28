---
id: ELITEA-2922
title: "Authorize action completes OAuth and resumes the original tool call automatically"
priority: critical
type: functional
module: toolkit-authorization
status: draft
execution_type: manual
tags: [feat:mcp-remote, feat:toolkits, int:openapi, int:sharepoint, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6072]
---

## Preconditions

- User is logged in to `{{base_url}}`
- At least one OAuth-requiring toolkit (SharePoint delegated, OpenAPI delegated, or Remote MCP) with no valid token, added to a chat
- Valid OAuth credentials/account available to complete the login flow in the browser popup/redirect

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Toolkit under test | SharePoint (Delegated) — repeat for OpenAPI (Delegated) and Remote MCP as data variants |
| Trigger message | A message invoking a tool from the toolkit |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a message that triggers the toolkit's tool call | "Toolkit Authorization Required" popup appears, tool call paused |
| 2 | Click **Authorize** | Browser OAuth flow opens (new tab/redirect) |
| 3 | Complete the OAuth login/consent in the flow | OAuth flow completes successfully and control returns to the chat |
| 4 | Observe the chat without resending the original message | The originally requested tool call executes automatically and a result streams into the conversation |

## Expected Final State

After completing OAuth via Authorize, the chat automatically resumes and executes the original tool call — the user is not required to resend their message — and a result is streamed to the conversation.

## Pass/Fail Criteria

**Pass:**
- Authorize opens a functional OAuth flow
- On successful OAuth completion, control returns to chat automatically
- The original tool call executes and streams a result without user resending the message

**Fail:**
- Authorize does not open an OAuth flow, or the flow fails to complete
- After successful OAuth, the tool call does not resume automatically (requires manual resend)
- No result streams after authorization completes
