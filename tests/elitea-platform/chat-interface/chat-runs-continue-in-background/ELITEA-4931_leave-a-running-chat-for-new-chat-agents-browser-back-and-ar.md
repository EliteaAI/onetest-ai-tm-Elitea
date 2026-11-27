---
id: ELITEA-4931
title: "Leave a running chat for New chat, Agents, browser Back and Artifacts, then see the New response dot"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** Every way of leaving a running chat (New chat, left menu, browser Back, Artifacts) keeps the run going, and a run that ends while you are away marks its row with the New response dot.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385LongRunner as the participant, cleared
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message in A | `The word is SMK2.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and wait for the first step | The run is going |
| 2 | Click **New chat** | An empty chat opens at once and its composer is enabled |
| 3 | Open **Agents** in the left menu | The Agents page opens at once |
| 4 | Click the browser Back button, then open **Artifacts** | Each page opens at once. No "Response generation is still in progress…" dialog and no "Output is still generating" text anywhere |
| 5 | Stay away until the run has ended (about 45 s from the send), then open the chat list in-app (New chat → chat list) | A's row shows the dot with the tooltip "New response" |
| 6 | Open A | The answer `RUN-DONE SMK2` and all 5 steps are shown; no streaming indicator. The dot is gone and stays gone |

**Note:** Come back to the chat list in-app. A page reload drops the New response dot, because it is held in the browser only.

## Expected Final State

The run finished while the user was on other pages, and the row marked the new answer until it was opened.

## Pass/Fail Criteria

**Pass:**
- No dialog and no `DELETE /task` for any of the four navigations
- The New response dot appears after the end and clears on open
- A shows the full answer and 5 steps

**Fail:**
- Any navigation shows a dialog, is delayed, or stops the run
- No dot, or the dot stays after A is opened
