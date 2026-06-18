---
id: ELITEA-0717
title: "Agent Chat: index_data Completes Without Failure When Bucket Contains Skipped Files"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:3672, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3672]
---
# ELITEA-0717: Agent Chat: index_data Completes Without Failure When Bucket Contains Skipped Files

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an Agent with an Artifact Toolkit is invoked via Chat to run `index_data` on a mixed-file bucket, the tool call completes (not "Tool execution failed") and the Agent's response reflects the indexing outcome.

**Coverage:**
- `index_data` tool chipset reaches completion state — not ❌ failed — when files are skipped
- No error traceback displayed in chipset due to skipped files
- Agent final response contains indexing outcome (indexed count or skipped mention)

## Preconditions

- Logged in to {{base_url}}
- Agent created with Artifact Toolkit attached (pointing to `mixed-files-test`: 5 valid + 3 problematic files)

## Test Data

- Agent prompt: "Index the mixed-files-test bucket with collection suffix agent-skip-test."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Chat conversation with the Agent. | Chat input is active. Agent is loaded. |
| 2 | Send: "Index the mixed-files-test bucket with collection suffix ag_skp." | Agent processes the request. A tool chipset for `index_data` appears. |
| 3 | Observe the `index_data` chipset state while the run is In Progress. | Chipset shows 🔄 In Progress — no immediate failure. |
| 4 | Wait for the run to complete. Check the final chipset state. | Chipset shows a completed state — NOT ❌ "Tool execution failed". |
| 5 | Read the Agent's final response in the Chat conversation. | Response contains the indexing outcome — at minimum the indexed count, ideally a mention of skipped files. |

## Expected Final State

Response contains the indexing outcome — at minimum the indexed count, ideally a mention of skipped files.

## Pass/Fail Criteria

**Pass:**
- `index_data` chipset reaches completion without ❌ failed state
- No error traceback in chipset output due to skipped files
- Agent response reflects indexing outcome

**Fail:**
- Chipset shows ❌ "Tool execution failed" caused by skipped files
- Full exception traceback shown to the user in the chipset
- Agent reports zero indexed count without acknowledging skipped files
