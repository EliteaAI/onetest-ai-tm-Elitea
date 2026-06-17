---
id: ELITEA-1004
title: "Non-Sensitive Tool Executes Without Authorization Dialog"
priority: high
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1004: Non-Sensitive Tool Executes Without Authorization Dialog

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that tools NOT configured as sensitive in Guardrails execute immediately and without any authorization dialog appearing.

## Preconditions

- github > create_pull_request is configured as sensitive
- github > get_pull_request (or another READ-ONLY GitHub tool) is NOT configured as sensitive
- Agent with the GitHub toolkit is open

## Test Data

- Non-sensitive tool to invoke: github > get_pull_request (or get_repository)
- Prompt: 'Get the details of pull request #1 in repo elitea/backend-api'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send the prompt that triggers the non-sensitive GitHub tool (get_pull_request): 'Get the details of pull request #1 in repo elitea/backend-api'. | Agent begins processing. |
| 2 | Observe the chat area for any authorization dialog. | No authorization dialog appears at any point. |
| 3 | Verify the agent returns the expected result from the tool call. | Tool executes immediately. Agent returns the pull request details. |

## Expected Final State

Tool executes immediately. Agent returns the pull request details.

## Pass/Fail Criteria

Pass:
- No authorization dialog shown for the non-sensitive tool
- Tool executes immediately and returns expected result
- Agent response completes normally

Fail:
- Authorization dialog appears for a non-sensitive tool
- Tool is incorrectly blocked or intercepted
