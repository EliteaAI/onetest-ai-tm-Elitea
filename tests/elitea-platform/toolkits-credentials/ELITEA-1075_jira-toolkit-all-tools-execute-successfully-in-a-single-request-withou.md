---
id: ELITEA-1075
title: "Jira Toolkit — All Tools Execute Successfully in a Single Request Without SDK Error"
priority: critical
type: functional
module: toolkits-credentials
status: ready
execution_type: manual
tags: [feat:toolkits, int:jira, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4931]
---
# ELITEA-1075: Jira Toolkit — All Tools Execute Successfully in a Single Request Without SDK Error

**Module:** Toolkits Credentials · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that triggering all Jira Toolkit tools in a single chat request — including approving sensitive tool executions — completes without an InternalSDKError or BadRequestError about missing `tool_call_id` responses.

**Bug Reference:** EliteaAI/elitea_issues#4931 — SDK error when executing all Jira Toolkit tools in a single request. The error (`AzureException BadRequestError: An assistant message with 'tool_calls' must be followed by tool messages responding to each 'tool_call_id'`) was consistently reproduced when all Jira tools were triggered at once and sensitive tools required manual approval.

**Coverage:**
- All Jira Toolkit tools are triggered in one request
- Sensitive tool executions are approved when prompted
- All tool calls complete without AzureException BadRequestError
- No missing `tool_call_id` warnings or InternalSDKError in the chat response
- Chat session ends with a successful response, not an error state

## Preconditions

- Logged in to {{base_url}}
- A Jira Toolkit is configured with valid Jira credentials (URL, token, project access)
- The toolkit includes sensitive tools that require manual approval before execution

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a new chat session in ELITEA | Chat input is ready |
| 2 | Attach the Jira Toolkit to the chat session (ensure valid Jira credentials are configured) | Jira Toolkit is attached and listed in the chat toolbar |
| 3 | Send a prompt that triggers execution of all available Jira tools (e.g., 'Run all available Jira tools on project X') | The LLM begins invoking multiple Jira tool calls in parallel or sequence |
| 4 | Approve all sensitive tool executions when prompted (click Approve for each one as it appears) | Each sensitive tool prompt is acknowledged; tool calls proceed after approval |
| 5 | Wait for all tool calls to complete and observe the final chat response | Chat completes successfully — no InternalSDKError, no BadRequestError, and no 'Missing tool_call_ids' message. All tool responses are properly matched and a coherent summary is returned. |

## Expected Final State

Chat completes successfully — no InternalSDKError, no BadRequestError, and no 'Missing tool_call_ids' message. All tool responses are properly matched and a coherent summary is returned.

## Pass/Fail Criteria

**Pass:**
- All Jira tool calls complete without error
- No `AzureException BadRequestError` or `InternalSDKError` is thrown
- No missing `tool_call_id` warnings appear
- Chat returns a coherent final response

**Fail:**
- Chat ends with an InternalSDKError or BadRequestError
- One or more `tool_call_id` values are reported as missing
- Sensitive tool approval flow causes tool response messages to be dropped from the chain
