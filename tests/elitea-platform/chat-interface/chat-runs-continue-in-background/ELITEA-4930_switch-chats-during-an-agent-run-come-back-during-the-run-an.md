---
id: ELITEA-4930
title: "Switch chats during an agent run, come back during the run and after it ends"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
known_issues: [elitea_issues#7763]
---

**Objective:** Leaving a running chat doesn't stop the run, and coming back shows the run live: the steps finished while away, Stop, "Agent is running…", and new steps as they happen.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385LongRunner as the participant, cleared
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message in A | `The word is SMK1.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message | The run starts and the first tool step appears |
| 2 | After the first step, click B in the chat list | B opens at once. No dialog, and the network log has no `DELETE /task/...` |
| 3 | Look at A's row in the chat list | The row shows the running spinner with the tooltip "Generating…" |
| 4 | Open A again while the run is still going | A shows the steps that finished while you were away, each with its tool name, plus the Stop button and "Agent is running…" |
| 5 | Stay in A until the run ends | New steps appear live as they start, the running step has a spinner, and the answer ends with `RUN-DONE SMK1` |
| 6 | Open B, then open A again | A shows the final answer and 5 steps; no streaming indicator. A's row shows no spinner |
| 7 | Call `GET {{base_url}}/api/v2/elitea_core/message_traces/prompt_lib/{project_id}/{conversation_id}` | 5 traces, the same steps in the same order as the UI |

## Expected Final State

The run in A finished normally, and the live view after the return matched the server.

## Pass/Fail Criteria

**Pass:**
- The run isn't stopped by leaving
- On return, the finished steps, Stop and "Agent is running…" are shown, and later steps render live
- After the end the UI shows 5 steps = `message_traces`

**Fail:**
- A dialog appears or `DELETE /task` is sent on leave
- After the return, new steps appear only together with the final answer, or the restored steps have no tool name (known issue #7763)
- The spinner stays in the row after the end
