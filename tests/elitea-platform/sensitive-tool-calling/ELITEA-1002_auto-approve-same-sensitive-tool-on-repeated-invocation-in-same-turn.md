---
id: ELITEA-1002
title: "Auto-Approve Same Sensitive Tool on Repeated Invocation in Same Turn"
priority: high
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-1002: Auto-Approve Same Sensitive Tool on Repeated Invocation in Same Turn

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that if the same sensitive tool is called twice in one conversation turn, and the first invocation is authorized, the second invocation of the same tool in the same turn is auto-approved without prompting a second dialog.

## Preconditions

- github > create_pull_request configured as sensitive
- Agent will call create_pull_request twice in a single turn (e.g., with different parameters)

## Test Data

- Prompt designed to cause the agent to call create_pull_request twice in succession

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send a prompt causing the agent to invoke create_pull_request twice. | Agent processes. First authorization dialog appears. |
| 2 | Click [Authorize] on the first dialog. | First dialog closes. First tool call executes. |
| 3 | Observe whether a second dialog appears for the second create_pull_request call. | No second authorization dialog appears. The second invocation of the same tool is auto-approved. |
| 4 | Agent completes its response. | Both PRs are created (one explicitly authorized, one auto-approved from same-turn authorization). |

## Expected Final State

Both PRs are created (one explicitly authorized, one auto-approved from same-turn authorization).

## Pass/Fail Criteria

Pass:
- Only one dialog shown for the same tool invoked twice in one turn
- Second invocation is auto-approved transparently
- Both tool executions succeed

Fail:
- Second dialog shown for the same tool within the same turn
- Auto-approval not working — user must re-authorize each time for the same tool
