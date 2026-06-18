---
id: ELITEA-1063
title: "Read multiple files remains usable from agent conversation after fix (regression)"
priority: high
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [feat:toolkits, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5002]
---
# ELITEA-1063: Read multiple files remains usable from agent conversation after fix (regression)

**Module:** Toolkits Credentials · **Priority:** High · **Type:** Functional

**Objective:** Verify that the "Read multiple files" tool still executes correctly when invoked through an agent conversation, confirming the Tooltip fix did not break the previously working path.

**Coverage:**
- Agent invokes Read multiple files tool successfully
- File contents are returned in the agent response
- No regression introduced in the agent/chat execution path

## Preconditions

- Logged into {{base_url}}
- An agent exists (or can be created) with an Artifact toolkit attached that has "Read multiple files" enabled
- At least one file (e.g. test.txt) exists in the toolkit's bucket

## Test Data

- Agent: any agent with Artifact toolkit (Read multiple files enabled) attached
- Prompt: "Please read the files test.txt from the artifact bucket."
- Expected file: test.txt in the Artifact bucket

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents and open an agent that has an Artifact toolkit (with 'Read multiple files' enabled) attached. | Agent detail page or agent chat is displayed. |
| 2 | Start a conversation and send: 'Please read the files test.txt from the artifact bucket.' | Agent processes the request and invokes the Read multiple files tool (visible in tool call trace if expanded). |
| 3 | Wait for the agent response. | Response contains the content of test.txt. No crash or JS error overlay occurs anywhere in the UI during or after the conversation. |

## Expected Final State

Response contains the content of test.txt. No crash or JS error overlay occurs anywhere in the UI during or after the conversation.

## Pass/Fail Criteria

**Pass:**
- Agent successfully invokes "Read multiple files" and returns file content
- No crash or JS error occurs in the UI during the conversation

**Fail:**
- Agent fails to call the tool or returns an error unrelated to file content
- UI crashes during or after the agent's tool invocation
