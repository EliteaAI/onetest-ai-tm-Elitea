---
id: ELITEA-4955
title: "An Ask User question reached while away waits on the chat row and can be answered on return"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

# ELITEA-4955: An Ask User question reached while away waits on the chat row and can be answered on return

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** If the agent asks the user a question while they are in another chat, the row shows that it is waiting, and the question card can be answered when the user comes back.

---

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385AskUser** ([instructions](../../../../test-data/chat-runs-continue/r7385-askuser.instructions.md)), internal tool Ask User on: waits 10 s, asks "Which JSONPlaceholder post should I look up?" (Post 1 / Post 2), answers `ASK-DONE post <id>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385AskUser as the participant, cleared
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

---

## Test Data

| Field | Value |
|-------|-------|
| Message in A | `Look up a post for me.` |
| Answer | Post 2 (its author is Leanne Graham) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and click B at once (during the 10 s wait) | B opens; no dialog |
| 2 | Wait until the run pauses (about 15 s), then look at A's row | The row shows the dot with the tooltip "Waiting for your answer" |
| 3 | Open A | The Clarifying Question card "Which JSONPlaceholder post should I look up?" is shown and enabled |
| 4 | Pick **Post 2** and click Continue | The run resumes and A's row spins again |
| 5 | Wait for the end | The answer is `ASK-DONE post 2` with the author Leanne Graham. The steps are `waitSeconds`, `ask_user`, `getPost`, `getUser` |

---

## Expected Final State

The question asked while away was answered on return and the run completed.

---

## Pass/Fail Criteria

**Pass:**
- Waiting dot on the row
- The card is shown, enabled, and resumes the run

**Fail:**
- No waiting dot, the card is missing or disabled on return, or answering doesn't resume the run

---

## Notes

- **Source functional tests:** ELITEA-4932 (`tests/elitea-platform/chat-interface/chat-runs-continue-in-background/`)
- **Regression rationale:** A question asked while the user is away must wait on the row and be answerable on return.
- **Selectors (`data-testid`):** `chat-list-item-unread-badge` with `data-reason=waiting` (tooltip "Waiting for your answer")
- Clear the fixture conversations before each run (`DELETE {{base_url}}/api/v2/elitea_core/messages/prompt_lib/{project_id}/{conversation_id}`). Otherwise the agent may reuse earlier results and skip its tools.
- Return to the chat list in-app (New chat → `sidebar-toggle`), never with `page.goto` or a reload: the New response dot is held in the browser only, and a reload drops it.
- Leave the running chat with a real click in the chat list, not a URL change.
- Use the API as the oracle: the conversation (`is_streaming`), `message_traces` for the steps, and `GET {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}?limit=100` for `has_running_task`. Watch the network log for `DELETE .../elitea_core/task/...`.
- Before sending, wait until `chat-switch-participant-button` shows the agent's name. Picking the agent adds it as a participant first and makes it active a moment later; a message sent in between goes to the default assistant, which has no tools.
- The chat URL gets `?name=<conversation name>` appended. Match `/chat/<id>` as a pattern, not the exact URL.
- Stop is an icon-only button next to the composer, with no testid and no `aria-label`. `chat-inject-button` is "Send to the running agent" (a message into the running turn), not Stop.
- After a finished chat is reopened, its steps sit in a collapsed "Thought for …" section (`chat-answer-thought-accordion`, toggle = its inner `button[aria-expanded]`). Expand it before counting steps.
- `message_traces` also returns one `thinking_step` row. Count only the rows with `kind` = `tool_call`.
- The pause is visible in the API as the message group's `is_streaming: false` and the socket `chat_run_status` `waiting`.
