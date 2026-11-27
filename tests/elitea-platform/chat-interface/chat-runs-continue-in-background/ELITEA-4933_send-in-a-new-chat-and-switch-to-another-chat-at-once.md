---
id: ELITEA-4933
title: "Send in a new chat and switch to another chat at once"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** Switching away right after Send in a brand-new chat (before the first chunk) still creates the chat and completes the run.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `#R7385LongRunner The word is SMK4.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click **New chat**, pick R7385LongRunner with `#`, and type the message | The agent is the participant |
| 2 | Click Send, and click B in the chat list within about 1 s | B opens and the user stays on B |
| 3 | Look at the chat list | The new chat appears with its generated name and the running spinner |
| 4 | Wait for the run to end (about 45 s), then open the new chat | It shows the user message and the answer `RUN-DONE SMK4` |

## Expected Final State

The new chat exists with both messages, although the user left it before the first chunk.

## Pass/Fail Criteria

**Pass:**
- The new chat is created and listed with a spinner
- The run completes with `RUN-DONE SMK4`

**Fail:**
- The chat isn't created, the user is pulled back to it, or the run is lost
