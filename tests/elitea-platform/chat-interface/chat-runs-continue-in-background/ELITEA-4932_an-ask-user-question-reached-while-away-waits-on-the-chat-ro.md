---
id: ELITEA-4932
title: "An Ask User question reached while away waits on the chat row and can be answered on return"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** If the agent asks the user a question while they are in another chat, the row shows that it is waiting, and the question card can be answered when the user comes back.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385AskUser** ([instructions](../../../../test-data/chat-runs-continue/r7385-askuser.instructions.md)), internal tool Ask User on: waits 10 s, asks "Which JSONPlaceholder post should I look up?" (Post 1 / Post 2), answers `ASK-DONE post <id>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385AskUser as the participant, cleared
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message in A | `Look up a post for me.` |
| Answer | Post 2 (its author is Leanne Graham) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and click B at once (during the 10 s wait) | B opens; no dialog |
| 2 | Wait until the run pauses (about 15 s), then look at A's row | The row shows the dot with the tooltip "Waiting for your answer" |
| 3 | Open A | The Clarifying Question card "Which JSONPlaceholder post should I look up?" is shown and enabled |
| 4 | Pick **Post 2** and click Continue | The run resumes and A's row spins again |
| 5 | Wait for the end | The answer is `ASK-DONE post 2` with the author Leanne Graham. The steps are `waitSeconds`, `ask_user`, `getPost`, `getUser` |

## Expected Final State

The question asked while away was answered on return and the run completed.

## Pass/Fail Criteria

**Pass:**
- Waiting dot on the row
- The card is shown, enabled, and resumes the run

**Fail:**
- No waiting dot, the card is missing or disabled on return, or answering doesn't resume the run
