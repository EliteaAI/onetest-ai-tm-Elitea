---
id: ELITEA-0997
title: "Guardrails Config with All Tools Unchecked — No Interception Occurs"
priority: medium
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-0997: Guardrails Config with All Tools Unchecked — No Interception Occurs

**Module:** Sensitive Tool Calling · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when no tools are selected as sensitive in the configuration (empty config), all tool invocations proceed normally without any authorization dialog.

## Preconditions

- All tools unchecked in Admin UI → Configuration → Guardrails
- Configuration saved and services restarted

## Test Data

- Any toolkit tool (e.g., github > create_pull_request) that was previously sensitive but is now unchecked
- Agent with the GitHub toolkit available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Admin UI → Guardrails, uncheck all previously checked tools. Clear company name. Save. Restart services. | Configuration saved with no sensitive tools. |
| 2 | Open the agent with the GitHub toolkit. Send a prompt to create a pull request. | Agent processes the request. |
| 3 | Observe the chat area. | No authorization dialog appears. The tool executes immediately. |
| 4 | Verify the expected side effect (PR created in GitHub). | PR created without any user intervention — no auth dialog shown. |

## Expected Final State

PR created without any user intervention — no auth dialog shown.

## Pass/Fail Criteria

Pass:
- No authorization dialog shown with empty sensitive tool config
- All tools execute immediately without interruption

Fail:
- Authorization dialog still appears after unchecking all tools and saving
