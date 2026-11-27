---
id: ELITEA-4942
title: "Stop a run after coming back, before any answer text"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** Stop still works on a run the user came back to, and the chat ends in the same state as the server.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385LongRunner as the participant, cleared
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `The word is H10.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and wait for the first step | The run is going (the agent writes answer text only at the end) |
| 2 | Open B, then open A again while it runs | Stop and "Agent is running…" are shown |
| 3 | Click **Stop** at once | Exactly one `DELETE /task/...` is sent, for this run |
| 4 | Look at A and call the conversation API | As today for Stop with no answer text: with thinking text it becomes the answer; with none, the user message and the answer are removed. The UI matches the server either way |
| 5 | Wait 15 s | No Stop button, no spinner, and the run doesn't restart |

## Expected Final State

The run was stopped from the returned view; nothing is left running.

## Pass/Fail Criteria

**Pass:**
- One `DELETE /task` for this run
- The UI matches the server state after Stop

**Fail:**
- Stop is missing, does nothing, stops another run, or leaves a spinner or Stop behind
