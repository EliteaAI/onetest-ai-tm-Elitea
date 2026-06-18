---
id: ELITEA-1001
title: "Agent Can Still Use Non-Blocked Tools After Blocking a Sensitive Tool"
priority: high
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1001: Agent Can Still Use Non-Blocked Tools After Blocking a Sensitive Tool

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that after the user blocks a sensitive tool, the agent can continue processing and use other non-blocked tools in the same turn, rather than stopping entirely.

## Preconditions

- github > create_pull_request configured as sensitive
- A non-sensitive tool (e.g., github > get_repository) is also available in the same agent

## Test Data

- Prompt: 'First, get the details of repo elitea/backend-api, and then create a pull request from feature/block-test to main'

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send the prompt. Agent first calls get_repository (non-sensitive). | get_repository executes without a dialog. |
| 2 | Agent then calls create_pull_request (sensitive). Authorization dialog appears. | Dialog shown for create_pull_request. |
| 3 | Click [Block]. | Dialog closes. create_pull_request is blocked. |
| 4 | Observe the agent's subsequent behavior. | Agent produces a response acknowledging the block. No additional invocation of create_pull_request. |
| 5 | Observe if the agent can still reference the result from get_repository. | Agent's response incorporates the successful get_repository result obtained earlier in the same turn. |

## Expected Final State

Agent's response incorporates the successful get_repository result obtained earlier in the same turn.

## Pass/Fail Criteria

Pass:
- Non-sensitive tool runs without dialog
- Blocking the sensitive tool leaves the agent functional for that turn
- Agent response references the result from the non-sensitive tool that ran successfully

Fail:
- Blocking one tool causes the entire agent execution to fail
- Agent becomes unresponsive after a Block
