---
id: ELITEA-4955
title: "An Ask User question reached while away waits on the chat row and can be answered on return"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_chat_ask_user_while_away.TestAskUserWhileAway.test_ask_user_while_away
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/5c07914a83fae0cf695e2fa5a19e7dfa15748cee
tags: [automated:UI:regression, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

# ELITEA-4955: An Ask User question reached while away waits on the chat row and can be answered on return

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** If the agent asks the user a question while they are in another chat, the row shows that it is waiting, and the question card can be answered when the user comes back.

---

## Preconditions

- User is logged in to `{{base_url}}` and has a project (`{project_id}`). Nothing else is needed: the test creates its own toolkits, agent and conversations in **Setup** and deletes them in **Teardown**. It never uses entities left by other tests or earlier runs. The source files are in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

---

## Test Data

| Field | Value |
|-------|-------|
| Run suffix `<sfx>` | 6 random hex characters, new for every run |
| Message in A | `Look up a post for me.` |
| Answer | Post 2 (its author is Leanne Graham) |

---

## Setup

Every name carries the run suffix `<sfx>` from Test Data, so parallel or repeated runs never meet.

| # | Action | Expected Result |
|---|--------|-----------------|
| S1 | Create two OpenAPI toolkits without credentials (`POST {{base_url}}/api/v2/elitea_core/tools/prompt_lib/{project_id}`): `autotest_echo_<sfx>` from [postman-echo-delay.openapi.yaml](../../../../test-data/chat-runs-continue/postman-echo-delay.openapi.yaml) with the tool `waitSeconds`, and `autotest_jph_<sfx>` from [jsonplaceholder.openapi.yaml](../../../../test-data/chat-runs-continue/jsonplaceholder.openapi.yaml) with the tools `getPost` and `getUser` | Both toolkits are created; note their ids |
| S2 | Create the agent `autotest_askuser_<sfx>` (`POST {{base_url}}/api/v2/elitea_core/applications/prompt_lib/{project_id}`) with the instructions from [r7385-askuser.instructions.md](../../../../test-data/chat-runs-continue/r7385-askuser.instructions.md), the project's default model, reasoning effort low, step limit 25, and the internal tool **Ask User** on (`meta.internal_tools: ["ask_user"]`) | The agent is created; note its id and version id. It waits 10 s, asks "Which JSONPlaceholder post should I look up?" (Post 1 / Post 2) and answers `ASK-DONE post <id>` |
| S3 | Link both toolkits to the agent's version with the tools above (`PATCH {{base_url}}/api/v2/elitea_core/tool/prompt_lib/{project_id}/{toolkit_id}`) | The agent's toolkits list shows both toolkits |
| S4 | Create the conversations `autotest_ask_A_<sfx>` and `autotest_idle_B_<sfx>` (`POST {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}`), then add the agent as the participant of A (in the UI, or `POST {{base_url}}/api/v2/elitea_core/participants/prompt_lib/{project_id}/{conversation_id}`) | The conversations are listed in the chat list and A has only the agent as participant |

---

## Steps

- Below, **A** is `autotest_ask_A_<sfx>` and **B** is the idle `autotest_idle_B_<sfx>` (no run in it).

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

## Teardown

Always run it, also when a step fails (for example in a `finally` block or a fixture finalizer). A failed delete is logged and doesn't change the verdict.

1. If a run is still going (the test failed midway), stop it first
2. Delete the conversations A and B (`DELETE {{base_url}}/api/v2/elitea_core/conversation/prompt_lib/{project_id}/{conversation_id}`)
3. Delete the agent (`DELETE {{base_url}}/api/v2/elitea_core/application/prompt_lib/{project_id}/{agent_id}`)
4. Delete both toolkits (`DELETE {{base_url}}/api/v2/elitea_core/tool/prompt_lib/{project_id}/{toolkit_id}`)
5. Check that none of the entities created by this run is left in the project

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
- **Stateless:** each run creates fresh entities and deletes them. Don't reuse a conversation from an earlier run: the agent may reuse the earlier tool results and skip its tools.
- Return to the chat list in-app (New chat → `sidebar-toggle`), never with `page.goto` or a reload: the New response dot is held in the browser only, and a reload drops it.
- Leave the running chat with a real click in the chat list, not a URL change.
- Use the API as the oracle: the conversation (`is_streaming`), `message_traces` for the steps, and `GET {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}?limit=100` for `has_running_task`. Watch the network log for `DELETE .../elitea_core/task/...`.
- Before sending, wait until `chat-switch-participant-button` shows the agent's name. Picking the agent adds it as a participant first and makes it active a moment later; a message sent in between goes to the default assistant, which has no tools.
- The chat URL gets `?name=<conversation name>` appended. Match `/chat/<id>` as a pattern, not the exact URL.
- Stop is an icon-only button next to the composer, with no testid and no `aria-label`. `chat-inject-button` is "Send to the running agent" (a message into the running turn), not Stop.
- After a finished chat is reopened, its steps sit in a collapsed "Thought for …" section (`chat-answer-thought-accordion`, toggle = its inner `button[aria-expanded]`). Expand it before counting steps.
- `message_traces` also returns one `thinking_step` row. Count only the rows with `kind` = `tool_call`.
- The pause is visible in the API as the message group's `is_streaming: false` and the socket `chat_run_status` `waiting`.
