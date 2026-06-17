---
id: ELITEA-1203
title: "TC-015: Agent Using Existing Jira Toolkit Still Works After UI Reorganization"
priority: high
type: functional
module: jira-toolkit-configuration
status: draft
execution_type: manual
tags: [feat:toolkits, issue:4029, int:jira, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1203: TC-015: Agent Using Existing Jira Toolkit Still Works After UI Reorganization

**Module:** Jira Toolkit Configuration · **Priority:** High · **Type:** Functional

**Objective:** Regression test — verify that an Agent that was already configured with a Jira Toolkit before the UI reorganization still executes Jira-related tool calls successfully. The deployment of the UI change should not break any existing agent-toolkit wiring.

Coverage:
- Existing agent with Jira toolkit still loads and can be tested
- Agent chat with Jira tool invocation returns valid response
- No toolkit-related configuration errors on agent load

## Preconditions

- An Agent that was previously configured with a Jira Toolkit exists in the project
- Logged in as the agent owner

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the existing Agent that uses a Jira Toolkit | Agent opens without errors; Jira Toolkit appears correctly in agent configuration |
| 2 | Verify the Jira toolkit is still listed in the agent configuration | Toolkit is still attached with correct name; no wiring error |
| 3 | Start a chat session with the agent | Chat session starts successfully |
| 4 | Send a prompt that requires Jira tool usage (e.g., 'List open issues in project KEY') | Agent invokes the Jira tool and returns a valid response from Jira |

## Expected Final State

Agent invokes the Jira tool and returns a valid response from Jira

## Pass/Fail Criteria

PASS:
- Agent loads without toolkit-related errors
- Sending a Jira-related prompt triggers a successful Jira tool call and returns a valid response

FAIL:
- Agent fails to load / shows toolkit configuration error
- Jira tool call fails when invoked from the agent
- Agent response indicates it cannot use the Jira toolkit
