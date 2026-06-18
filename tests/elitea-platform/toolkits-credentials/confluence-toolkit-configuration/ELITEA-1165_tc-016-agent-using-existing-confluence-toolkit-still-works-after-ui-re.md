---
id: ELITEA-1165
title: "TC-016: Agent Using Existing Confluence Toolkit Still Works After UI Reorganization"
priority: high
type: functional
module: confluence-toolkit-configuration
status: draft
execution_type: manual
tags: [int:confluence, feat:toolkits, issue:4029, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4029]
---
# ELITEA-1165: TC-016: Agent Using Existing Confluence Toolkit Still Works After UI Reorganization

**Module:** Confluence Toolkit Configuration · **Priority:** High · **Type:** Functional

**Objective:** Regression test — verify that an Agent that was already configured with a Confluence Toolkit before the UI reorganization still executes Confluence-related tool calls successfully. The deployment of the UI change should not break any existing agent-toolkit wiring.

Coverage:
- Existing agent with Confluence toolkit still loads without errors
- Agent executes Confluence tool call and returns valid response
- No toolkit wiring or configuration errors

## Preconditions

- An Agent previously configured with a Confluence Toolkit exists in the project
- Logged in as the agent owner

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the existing Agent that uses a Confluence Toolkit | Agent opens without errors; Confluence Toolkit listed correctly in agent config |
| 2 | Verify the Confluence toolkit is still attached with correct name | No wiring error; toolkit name and config intact |
| 3 | Start a chat session with the agent | Chat session starts successfully |
| 4 | Send a prompt that requires Confluence tool usage (e.g., 'Search for pages about onboarding') | Agent invokes Confluence tool and returns a valid response from Confluence |

## Expected Final State

Agent invokes Confluence tool and returns a valid response from Confluence

## Pass/Fail Criteria

PASS:
- Agent opens without toolkit-related errors; Confluence toolkit correctly listed in config
- Sending a Confluence-related prompt triggers a successful tool call and returns a valid response

FAIL:
- Agent shows toolkit configuration error on load
- Confluence tool call fails from within the agent
- Agent cannot use the Confluence toolkit
