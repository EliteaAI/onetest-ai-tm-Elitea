---
id: ELITEA-2923
title: "Skip action cancels the specific toolkit call without breaking the rest of the conversation or other participants"
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
- A chat conversation has 2+ participants: one OAuth-requiring MCP/toolkit (no valid token) and at least one other working toolkit/agent

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Participants | 1 OAuth-requiring MCP (e.g. Atlassian Remote MCP) + 1 other functional participant (agent/toolkit) |
| Trigger message | A message invoking the MCP's tool among several attached participants |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send a message that triggers the OAuth-requiring MCP's tool call | "Toolkit Authorization Required" popup appears for that MCP |
| 2 | Click **Skip** | The toolkit call for that MCP is not executed; agent acknowledges the skipped action rather than retrying silently |
| 3 | Send a follow-up message that engages the other, unaffected participant | The other participant responds normally, unaffected by the earlier Skip |
| 4 | Review the conversation as a whole | Conversation remains fully usable — no broken state, no stuck pending indicators |

## Expected Final State

The skipped toolkit call remains unexecuted and acknowledged as skipped; the conversation and all other participants continue to function normally with no residual blocking state.

## Pass/Fail Criteria

**Pass:**
- Skip cancels only the specific toolkit call, no execution occurs
- Agent/chat visibly acknowledges the skip (no silent retry)
- Other participants remain fully responsive after the Skip

**Fail:**
- Skip causes the toolkit call to execute anyway, or silently retries
- Other participants become unresponsive or errored after the Skip
- Conversation is left in a stuck/pending state
