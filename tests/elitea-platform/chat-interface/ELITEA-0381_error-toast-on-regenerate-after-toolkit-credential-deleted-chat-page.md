---
id: ELITEA-0381
title: "Error Toast on Regenerate After Toolkit Credential Deleted (Chat Page)"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: automated
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4721, https://github.com/EliteaAI/elitea-testing/pull/130]
---
# ELITEA-0381: Error Toast on Regenerate After Toolkit Credential Deleted (Chat Page)

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking Regenerate on an agent message after the agent's toolkit credential is deleted triggers an error toast and preserves the previous response — when the agent is invoked from the Chat page.

**Coverage:**
- Agent with GitHub toolkit is configured and added to a Chat conversation
- Toolkit-backed response is received via Chat
- After credential deletion Regenerate triggers a server-side failure
- Error toast appears with the correct message
- Previous toolkit-backed response is preserved after failure
- Toast is visible for ≥5 seconds or until dismissed

## Preconditions

- Logged in to {{base_url}}
- A GitHub credential exists in the project
- Agent A exists with a GitHub toolkit configured using that credential

## Test Data

| Item | Value |
|---|---|
| Toolkit type | GitHub |
| Credential | Any existing GitHub credential attached to Agent A |
| Failure trigger | Delete the credential Agent A's toolkit depends on |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Chat page. Add Agent A as a participant in a conversation. | Agent A appears as a participant in the chat. |
| 2 | Send a message that invokes the GitHub toolkit (e.g., ask Agent A to list repositories or fetch a file). | Agent A returns a toolkit-backed response. Response is visible in the chat. |
| 3 | Navigate to Credentials and delete the GitHub credential that Agent A's toolkit depends on. | Credential is deleted. Agent A's toolkit is now misconfigured. |
| 4 | Return to the chat conversation from step 2. | Chat is still open. Previous toolkit-backed response is visible. |
| 5 | Click the Regenerate button on Agent A's message. | Regeneration request is sent. Toolkit lookup fails server-side (500 error). |
| 6 | Observe the UI after the request completes. | Error toast appears with the message "Regeneration Failed. Please try again." (at least 5 seconds) |
| 7 | Observe the chat message area. | Previous toolkit-backed response is still displayed. No blank or empty state appears. |

## Expected Final State

Previous toolkit-backed response is still displayed. No blank or empty state appears.

## Pass/Fail Criteria

**Pass:**
- Error toast appears with "Regeneration Failed. Please try again."
- Toast is visible for ≥5 seconds or until dismissed
- Previous toolkit-backed response is preserved in the chat

**Fail:**
- No toast shown — silent failure
- Chat message area goes blank
- Toast text is incorrect or missing
