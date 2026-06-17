---
id: ELITEA-1255
title: "index_data Without Path Triggered via Agent Chat Succeeds on Special-Character Libraries"
priority: high
type: functional
module: sharepoint
status: draft
execution_type: manual
tags: [int:sharepoint, feat:indexer, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3826]
---
# ELITEA-1255: index_data Without Path Triggered via Agent Chat Succeeds on Special-Character Libraries

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that when the SharePoint toolkit is attached to an ELITEA Agent and the agent is prompted via Chat to index all documents without specifying a path, the `index_data` call completes successfully — end-to-end integration via Agent and Chat.

**Coverage:**
- SharePoint toolkit attached to an Agent with Index Data tool enabled
- Agent invoked via Chat conversation
- `index_data` called with no path through the Agent
- Tool chipset in Chat shows success (no "Tool execution failed")
- No `AttributeError` traceback in chipset
- Agent final message confirms successful indexing

## Preconditions

- An Agent exists in the Private project with the SharePoint toolkit attached and Index Data tool enabled
- Chat conversation with the agent is open or can be started
- Special-character libraries exist on the SharePoint site per Pre-Testing Setup

## Test Data

- Agent prompt: "Index all documents from the SharePoint site with suffix 'chat'. Do not specify a path."
- Expected tool called: index_data
- Expected index suffix used: chat

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat | Chat interface is displayed |
| 2 | Open or create a conversation with the Agent that has the SharePoint toolkit attached | Conversation opens; SharePoint toolkit participates |
| 3 | Send the message: "Index all documents from the SharePoint site with suffix 'chat'. Do not specify a path." | Message is sent; agent begins processing |
| 4 | Observe the tool chipset that appears for the index_data call | Chipset expand/collapse is visible in the chat response |
| 5 | Click the chipset to expand it | Chipset content is displayed |
| 6 | Verify the chipset output does NOT contain "Tool execution failed" or AttributeError | No error traceback is present in the chipset |
| 7 | Wait for the agent's final response | Final response text is shown |
| 8 | Verify the final response confirms successful indexing | Agent reports successful indexing without error |
| 9 | Navigate to the SharePoint toolkit → Indexes tab and confirm the `chat` index appears with a non-zero total | `chat` index created; total indexed ≥ 1 |

## Expected Final State

`chat` index created; total indexed ≥ 1

## Pass/Fail Criteria

**Pass:**
- Chipset shows no error
- Agent final response confirms success
- `chat` index visible in Indexes tab with non-zero count

**Fail:**
- Chipset shows "Tool execution failed"
- `AttributeError` appears in chipset
- Agent reports failure or no index appears in the toolkit
