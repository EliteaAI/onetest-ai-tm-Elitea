---
id: ELITEA-4957
title: "Two chats run at once and Stop in one leaves the other running"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_chat_two_runs_stop_one.TestTwoChatsRunStopOneLeavesOther.test_two_chats_run_stop_one_leaves_other
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/ec1cfba7e19c698063c4c3b3a60c822141820f4b
tags: [automated:UI:regression, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

# ELITEA-4957: Two chats run at once and Stop in one leaves the other running

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** Runs in different chats are independent: both show the spinner, and Stop in one stops only that run.

---

## Preconditions

- User is logged in to `{{base_url}}` and has a project (`{project_id}`). Nothing else is needed: the test creates its own toolkits, agent and conversations in **Setup** and deletes them in **Teardown**. It never uses entities left by other tests or earlier runs. The source files are in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

---

## Test Data

| Field | Value |
|-------|-------|
| Run suffix `<sfx>` | 6 random hex characters, new for every run |
| Message in A | `The word is SMK5A.` |
| Message in C | `The word is SMK5C.` |

---

## Setup

Every name carries the run suffix `<sfx>` from Test Data, so parallel or repeated runs never meet.

| # | Action | Expected Result |
|---|--------|-----------------|
| S1 | Create two OpenAPI toolkits without credentials (`POST {{base_url}}/api/v2/elitea_core/tools/prompt_lib/{project_id}`): `autotest_echo_<sfx>` from [postman-echo-delay.openapi.yaml](../../../../test-data/chat-runs-continue/postman-echo-delay.openapi.yaml) with the tool `waitSeconds`, and `autotest_jph_<sfx>` from [jsonplaceholder.openapi.yaml](../../../../test-data/chat-runs-continue/jsonplaceholder.openapi.yaml) with the tools `getPost` and `getUser` | Both toolkits are created; note their ids |
| S2 | Create the agent `autotest_runner_<sfx>` (`POST {{base_url}}/api/v2/elitea_core/applications/prompt_lib/{project_id}`) with the instructions from [r7385-longrunner.instructions.md](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md), the project's default model, reasoning effort low, step limit 25 | The agent is created; note its id and version id. It runs about 45 s with 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`) and answers `RUN-DONE <word>` |
| S3 | Link both toolkits to the agent's version with the tools above (`PATCH {{base_url}}/api/v2/elitea_core/tool/prompt_lib/{project_id}/{toolkit_id}`) | The agent's toolkits list shows both toolkits |
| S4 | Create the conversations `autotest_run_A_<sfx>` and `autotest_run_C_<sfx>` (`POST {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}`), then add the agent as the participant of A and C (in the UI, or `POST {{base_url}}/api/v2/elitea_core/participants/prompt_lib/{project_id}/{conversation_id}`) | The conversations are listed in the chat list and A and C have only the agent as participant |

---

## Steps

- Below, **A** is `autotest_run_A_<sfx>` and **C** is `autotest_run_C_<sfx>`.

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the message in A, open C and send its message | Both rows show the running spinner |
| 2 | In C, wait for the first step and click **Stop** (square icon next to the composer) | Exactly one `DELETE /task/...` is sent, for C's run. The Stop button disappears, and C's row gets no dot |
| 3 | Open A | A's run is still going (Stop and "Agent is running…" shown) |
| 4 | Wait for A to end | A's answer is `RUN-DONE SMK5A` |

---

## Expected Final State

C was stopped; A finished normally.

---

## Teardown

Always run it, also when a step fails (for example in a `finally` block or a fixture finalizer). A failed delete is logged and doesn't change the verdict.

1. If a run is still going (the test failed midway), stop it first
2. Delete the conversations A and C (`DELETE {{base_url}}/api/v2/elitea_core/conversation/prompt_lib/{project_id}/{conversation_id}`)
3. Delete the agent (`DELETE {{base_url}}/api/v2/elitea_core/application/prompt_lib/{project_id}/{agent_id}`)
4. Delete both toolkits (`DELETE {{base_url}}/api/v2/elitea_core/tool/prompt_lib/{project_id}/{toolkit_id}`)
5. Check that none of the entities created by this run is left in the project

---

## Pass/Fail Criteria

**Pass:**
- Both rows spin at once
- Stop in C affects only C

**Fail:**
- Stop in C stops A or sends a request for A's run
- Either row is missing the spinner while its run is going

---

## Notes

- **Source functional tests:** ELITEA-4934 (`tests/elitea-platform/chat-interface/chat-runs-continue-in-background/`)
- **Regression rationale:** Runs in different chats must be independent: both spin, and Stop in one doesn't touch the other.
- **Selectors (`data-testid`):** `chat-list-item-running-icon` on both rows
- **Stateless:** each run creates fresh entities and deletes them. Don't reuse a conversation from an earlier run: the agent may reuse the earlier tool results and skip its tools.
- Return to the chat list in-app (New chat → `sidebar-toggle`), never with `page.goto` or a reload: the New response dot is held in the browser only, and a reload drops it.
- Leave the running chat with a real click in the chat list, not a URL change.
- Use the API as the oracle: the conversation (`is_streaming`), `message_traces` for the steps, and `GET {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}?limit=100` for `has_running_task`. Watch the network log for `DELETE .../elitea_core/task/...`.
- Before sending, wait until `chat-switch-participant-button` shows the agent's name. Picking the agent adds it as a participant first and makes it active a moment later; a message sent in between goes to the default assistant, which has no tools.
- The chat URL gets `?name=<conversation name>` appended. Match `/chat/<id>` as a pattern, not the exact URL.
- Stop is an icon-only button next to the composer, with no testid and no `aria-label`. `chat-inject-button` is "Send to the running agent" (a message into the running turn), not Stop.
- After a finished chat is reopened, its steps sit in a collapsed "Thought for …" section (`chat-answer-thought-accordion`, toggle = its inner `button[aria-expanded]`). Expand it before counting steps.
- `message_traces` also returns one `thinking_step` row. Count only the rows with `kind` = `tool_call`.
- Stop must send `DELETE .../elitea_core/task/prompt_lib/{project_id}/{run_uuid}` with C's run uuid only. Take each run uuid from the latest `chat_run_status` "running" socket frame of that chat.
- Related: ELITEA-2621 checks Stop isolation across two tabs or the widget. This case checks it within one tab while switching chats.
