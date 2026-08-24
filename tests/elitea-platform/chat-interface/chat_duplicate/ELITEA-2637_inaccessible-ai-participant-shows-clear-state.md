---
id: ELITEA-2637
title: "Duplicated Chat with Inaccessible AI Shows Clear State - No Silent Access Grant"
priority: low
type: functional
module: chat-interface
status: ready
execution_type: manual
automation_test_id: []
tags: [chat, duplicate, ai-error-state, P2]
requirements: [3837]
---
# ELITEA-2637: Duplicated Chat with Inaccessible AI Shows Clear State - No Silent Access Grant

**Module:** Chat Interface · **Priority:** Low · **Type:** Functional

**Objective:** Verify that a duplicated chat containing inaccessible tools, MCPs, or agents shows a clear configuration state and does not silently grant access to unavailable resources.

## Preconditions

- User is logged in to {{base_url}}
- Original chat exists with MCP or Agent that becomes unavailable
- MCP server is disconnected OR Agent has configuration errors

## Test Data

- URL: {{base_url}}
- Chat with:
  - Disconnected MCP participant (shows "Server is disconnected!")
  - OR Misconfigured Agent (shows "Misconfiguration errors found")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set up a chat with MCP participant | MCP added to chat |
| 2 | Disconnect the MCP server (or use pre-disconnected MCP) | MCP shows disconnected state/error indicator |
| 3 | OR use an Agent with configuration errors | Agent shows error indicator |
| 4 | Duplicate the chat containing the inaccessible AI | Duplicate created successfully |
| 5 | Open duplicated chat | Duplicated chat opens |
| 6 | Check Participants panel for MCP/Agent | Participant present in duplicate |
| 7 | Verify error state indicator is visible on MCP/Agent | Error indicator shown: "Server is disconnected!" OR "Misconfiguration errors found" |
| 8 | Attempt to use the disconnected MCP/Agent | Clear error message displayed |
| 9 | Verify no silent access granted | User cannot use unavailable resource |
| 10 | Verify error state persists (not auto-fixed) | Error indicator remains until manually fixed |

## Expected Final State

- Duplicated chat contains inaccessible AI participant
- Clear error indicator visible (disconnected/misconfigured)
- No silent access grant occurs
- User aware of unavailable state
- Explicit reconnection/fix required

## Pass/Fail Criteria

**Pass:**
- Error indicator visible on inaccessible AI
- Clear error message displayed
- No silent access granted
- User cannot use unavailable resource
- Error state accurately communicated

**Fail:**
- No error indicator shown
- Resource appears available but isn't
- Silent access grant attempted
- Error state hidden or unclear
- User misled about availability
