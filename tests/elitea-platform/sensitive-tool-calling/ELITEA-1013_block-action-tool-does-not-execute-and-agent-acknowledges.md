---
id: ELITEA-1013
title: "Block Action — Tool Does NOT Execute and Agent Acknowledges"
priority: critical
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1013: Block Action — Tool Does NOT Execute and Agent Acknowledges

**Module:** Sensitive Tool Calling · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that clicking [Block] closes the dialog, prevents the sensitive tool from executing, and the agent produces a response acknowledging the block — without retrying the blocked tool.

## Preconditions

- github > create_pull_request configured as sensitive
- Authorization dialog is currently displayed in the agent chat

## Test Data

- Tool being blocked: github.create_pull_request
- Verify no side effects: No PRs created in the target repository

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Ensure the authorization dialog is visible. | Dialog is displayed. |
| 2 | Click the [Block] button. | Dialog closes immediately. |
| 3 | Observe the agent's response in the chat. | Agent produces a text response acknowledging that the action was blocked by the user. |
| 4 | Verify in GitHub that no new PR was created in the target repository. | No pull request was created. The sensitive tool did not execute. |
| 5 | Observe agent behavior for any retry attempts of create_pull_request. | Agent does NOT attempt to invoke create_pull_request again in this turn. |
| 6 | Verify the chat input and Send button are re-enabled. | Input field is active. Send button is clickable. |
| 7 | Send a follow-up message in chat. | New message is sent and the agent responds normally. |

## Expected Final State

New message is sent and the agent responds normally.

## Pass/Fail Criteria

Pass:
- Dialog closes on clicking Block
- Tool does NOT execute (no PR created in GitHub)
- Agent text response acknowledges the block
- Agent does not retry the blocked tool
- Chat input and Send button re-enabled
- Follow-up messages work normally

Fail:
- Tool executes despite Block being clicked
- Agent produces no response after block
- Agent retries the blocked action
- Chat remains stuck (input disabled)
