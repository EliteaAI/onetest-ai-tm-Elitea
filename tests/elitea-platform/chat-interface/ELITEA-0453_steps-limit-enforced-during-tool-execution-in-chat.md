---
id: ELITEA-0453
title: "Steps Limit Enforced During Tool Execution in Chat"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3292]
---
# ELITEA-0453: Steps Limit Enforced During Tool Execution in Chat

**Module:** Chat Interface · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when Steps Limit is configured in Model Settings, tool execution stops at exactly the configured iteration count and the error message includes the configured limit value.

**Coverage:**
- Execution stops at exactly the configured number of tool iterations
- Error message text includes the configured steps limit value
- Expected error format: "Maximum tool execution iterations (N) reached. Stopping tool execution."
- Artifact Toolkit list-files operations are counted as individual tool calls

## Preconditions

- Logged in to {{base_url}}
- Private project selected
- Artifact Toolkit created and configured with access to the default bucket
- Browser: Chrome (latest)

## Test Data

- Steps Limit value: 3
- Participant: Artifact Toolkit (default bucket)
- Prompt: "list files from folder 3 times: after each listing find the file with the lowest size, if no files just proceed. Details: default bucket, recursive, analyze after each listing, then proceed without approval"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Create a new conversation and add an Artifact Toolkit as a participant. | Artifact Toolkit appears in the Participants panel. |
| 2 | Open the Model Settings modal (⚙ icon next to model selector). Set STEPS LIMIT to '3'. Click Apply. | Modal closes. Steps Limit is now set to 3. |
| 3 | Type the prompt in the chat input and send: 'list files from folder 3 times: after each listing find the file with the lowest size, if no files just proceed. Details: default bucket, recursive, analyze after each listing, then proceed without approval' | The AI begins executing tool calls. |
| 4 | Observe the chat response output as execution proceeds. | Execution stops. The response contains: 'Maximum tool execution iterations (3) reached. Stopping tool execution.' |

## Expected Final State

Execution stops. The response contains: 'Maximum tool execution iterations (3) reached. Stopping tool execution.'

## Pass/Fail Criteria

**Pass:**
- Execution stops at or before 3 tool iterations
- Error message explicitly shows the configured limit value (3)
- Error text matches: "Maximum tool execution iterations (3) reached. Stopping tool execution."

**Fail:**
- Execution continues beyond 3 tool iterations
- Error message shows a different limit value (e.g. 25)
- No error message is shown
- The chat freezes or crashes instead of showing the error
