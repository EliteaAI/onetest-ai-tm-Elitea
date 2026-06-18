---
id: ELITEA-0725
title: "[EliteaAI/elitea_issues#5116] MCP via Chat Conversation: Secret Field Shows \"New Secret\" Shortcut"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [feat:credentials, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5116]
---
# ELITEA-0725: [EliteaAI/elitea_issues#5116] MCP via Chat Conversation: Secret Field Shows "New Secret" Shortcut

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that when adding or configuring a Remote MCP from within a Chat conversation, secret fields in Secret mode expose the same "New Secret" shortcut as on the dedicated MCPs page — no inconsistency between entry points.

## Preconditions

- Logged in to ELITEA ({{base_url}}
- User has permissions to add MCPs to a Chat conversation and has secret create/list permissions
- A Remote MCP requiring OAuth2 auth (Client Secret field) is available to add

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Open any existing conversation or create a new one. | Chat conversation page is open. |
| 2 | Use the MCP addition flow in Chat to add a Remote MCP that requires an OAuth2 / token Client Secret field. | MCP configuration panel opens within the Chat interface. |
| 3 | In the MCP configuration panel, locate the Client Secret field. Switch it to Secret mode. | Client Secret field is in Secret mode with a combobox visible. |
| 4 | Open the secret dropdown. | Dropdown opens showing: (1) a CREATE section with the correct label ('New Private Secret' or 'New Project Secret' matching the project type); (2) a SAVED SECRETS section with a refresh icon. |
| 5 | Click the CREATE option. | Settings → Secrets opens in a new browser tab with ?createSecret=1. The Chat conversation tab remains open and unchanged. |

## Expected Final State

Settings → Secrets opens in a new browser tab with ?createSecret=1. The Chat conversation tab remains open and unchanged.

## Pass/Fail Criteria

**Pass:** CREATE section with correct label and refresh icon visible in the Chat-based MCP config; clicking CREATE opens new tab with ?createSecret=1 without disrupting the Chat conversation.
**Fail:** CREATE section absent specifically in the Chat entry point (inconsistency); wrong label; same tab navigates away; feature works on the MCPs dedicated page but not in Chat.
