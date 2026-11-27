---
id: ELITEA-4936
title: "Three chats run at once while the user switches between them"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** Three parallel runs started from three chats all spin in the list, and each ends with its own answer and steps.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- Conversations **X-A**, **X-B**, **X-C**, each with R7385LongRunner as the participant, cleared
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Words | `H02A`, `H02B`, `H02C` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send `The word is H02A.` in X-A, open X-B and send `The word is H02B.`, open X-C and send `The word is H02C.` (a few seconds apart) | Each send starts a run |
| 2 | Look at the chat list | All 3 rows show the running spinner at the same time |
| 3 | Wait for all 3 runs to end, then open each chat | X-A ends `RUN-DONE H02A`, X-B `RUN-DONE H02B`, X-C `RUN-DONE H02C`, each with its own 5 steps |
| 4 | Compare each chat's steps with `message_traces` of that chat | 5 traces each, matching the UI |

## Expected Final State

All three runs completed independently. No answer or step went to the wrong chat.

## Pass/Fail Criteria

**Pass:**
- All 3 rows spin at once
- Each chat has its own word and its own 5 steps
- No `DELETE /task` and no message was deleted

**Fail:**
- A run is stopped or lost, or answers/steps are mixed between chats
