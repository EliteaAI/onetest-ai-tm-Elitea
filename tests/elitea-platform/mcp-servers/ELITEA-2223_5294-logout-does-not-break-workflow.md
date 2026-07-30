---
id: ELITEA-2223
title: "[EliteaAI/elitea_issues#5294] Logout Does Not Break Workflow — Verify Chat/Agent/Pipeline unaffected"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [issue:5294, r-2.0.5, feat:mcp-remote, eng:backend, eng:frontend, nfr:usability, logout-button, mcp-auth]
requirements: [EliteaAI/elitea_issues#5294]
---

# ELITEA-2223: [EliteaAI/elitea_issues#5294] Logout Does Not Break Workflow

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that logging out from an MCP does not crash, break, or interrupt the Chat, Agent, or Pipeline workflow. The interface remains functional and responsive.

## Preconditions

- Logged in to ELITEA ({{base_url}})
- An active Chat conversation with MCP participant is open
- An active Agent with MCP toolkit is running in a chat conversation
- An active Pipeline with MCP toolkit node is configured and ready to execute
- All systems are in authenticated state

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Chat with MCP participant, send a message. MCP is invoked and responds. | Chat receives MCP response; conversation continues normally. |
| 2 | Click Logout button on the MCP toolbar. | Logout succeeds; no error; no page refresh occurs. |
| 3 | Send another message to the Chat (without invoking MCP). | Message sent successfully; Chat remains responsive; no errors in console. |
| 4 | Navigate to Agent-in-Chat interface. Run the Agent (which contains MCP toolkit). | Agent executes; returns response (MCP is not invoked or returns auth error gracefully). |
| 5 | After Agent execution, Chat remains open and interactive. User can send new messages. | Chat continues to function; no crashes; message sending works. |
| 6 | Navigate to Pipeline page. Execute a Pipeline that contains an MCP toolkit node. | Pipeline execution begins; reaches MCP node. |
| 7 | At MCP node, if MCP is unauthenticated, Pipeline handles error gracefully (halts at node or returns error message). | Pipeline does not crash; error is logged; node status shows "failed" or "awaiting authentication". |
| 8 | Check browser console for JavaScript errors (F12 → Console). | No unhandled exceptions; no red errors related to logout. |

## Expected Final State

- Chat continues to function after logout
- Agent-in-Chat can execute without crashing
- Pipeline executes without crashing (fails gracefully at MCP node if unauthenticated)
- No console errors or unhandled exceptions
- User can navigate and interact normally

## Pass/Fail Criteria

**Pass:** Logout does not break Chat/Agent/Pipeline; workflows continue normally; graceful error handling at MCP nodes.  
**Fail:** Logout causes crash, error, or unresponsiveness; Chat/Agent/Pipeline becomes unusable; unhandled exceptions in console.
