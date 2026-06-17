---
id: ELITEA-1015
title: "Verify Sensitive Tool Execution Intercepted in Agent Chat"
priority: critical
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1015: Verify Sensitive Tool Execution Intercepted in Agent Chat

**Module:** Sensitive Tool Calling · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when a tool is marked as sensitive in the Guardrails configuration, the LangChain middleware intercepts its execution in the Agent chat context and presents the authorization dialog before the tool runs.

## Preconditions

- Logged in as Platform Administrator
- github > create_pull_request is configured as a sensitive tool in Admin UI → Configuration → Guardrails and saved
- Services restarted after save
- An agent with the GitHub toolkit is open and ready to chat

## Test Data

- Sensitive tool: github.create_pull_request
- User prompt: "Create a pull request from branch 'feature/test-branch' to 'main' in repo 'elitea/backend-api' with title 'feat: Test PR'"
- Company name configured: EPAM

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. Enable github > create_pull_request as sensitive. Set Company Name to EPAM. Click Save Configuration. | Configuration saved. Success notification shown. |
| 2 | Restart services. | Services restarted successfully. |
| 3 | Navigate to the Agent page with the GitHub toolkit. | Agent detail page loads correctly. |
| 4 | Send the user prompt requesting a pull request creation. | Agent begins processing. |
| 5 | Observe the agent chat area before any tool execution occurs. | Authorization dialog appears with title '⚠️ Sensitive Action Authorization Required'. Tool has NOT executed yet. |
| 6 | Verify the dialog shows the action name github.create_pull_request prominently. | Action name is displayed in bold/prominent style. |
| 7 | Verify the dialog shows the Parameters section with at least repository, title, base_branch, head_branch fields. | Parameters section is visible with correct key-value pairs. |
| 8 | Verify the policy message reads: 'EPAM requires approval before running the sensitive action github.create_pull_request.' (or equivalent template). | Policy message is displayed correctly with the configured company name. |
| 9 | Verify both [Authorize] and [Block] buttons are present. | Both buttons are visible and appear clickable. |

## Expected Final State

Both buttons are visible and appear clickable.

## Pass/Fail Criteria

Pass:
- Authorization dialog appears before the tool executes
- Dialog is shown in the agent chat context
- Action name matches the configured sensitive tool
- Parameters section is visible
- Policy message includes the configured company name
- Both Authorize and Block buttons are present

Fail:
- Tool executes without showing any dialog
- Dialog appears after tool execution
- Dialog does not show correct action name
- Policy message missing or uses wrong company name
- Either Authorize or Block button is absent
