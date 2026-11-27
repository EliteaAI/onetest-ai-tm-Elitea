---
id: ELITEA-4956
title: "Send in a new chat and switch to another chat at once"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_chat_send_new_chat_switch_away.TestSendInNewChatAndSwitchAway.test_send_in_new_chat_and_switch_away_at_once
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/8eaf405c8ca5f4eeb0e6591f8cec6d307671cf85
tags: [automated:UI:regression, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

# ELITEA-4956: Send in a new chat and switch to another chat at once

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** Switching away right after Send in a brand-new chat (before the first chunk) still creates the chat and completes the run.

---

## Preconditions

- User is logged in to `{{base_url}}` and has a project (`{project_id}`). Nothing else is needed: the test creates its own toolkits, agent and conversations in **Setup** and deletes them in **Teardown**. It never uses entities left by other tests or earlier runs. The source files are in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

---

## Test Data

| Field | Value |
|-------|-------|
| Run suffix `<sfx>` | 6 random hex characters, new for every run |
| Message | `#autotest_runner_<sfx> The word is SMK4.` |

---

## Setup

Every name carries the run suffix `<sfx>` from Test Data, so parallel or repeated runs never meet.

| # | Action | Expected Result |
|---|--------|-----------------|
| S1 | Create two OpenAPI toolkits without credentials (`POST {{base_url}}/api/v2/elitea_core/tools/prompt_lib/{project_id}`): `autotest_echo_<sfx>` from [postman-echo-delay.openapi.yaml](../../../../test-data/chat-runs-continue/postman-echo-delay.openapi.yaml) with the tool `waitSeconds`, and `autotest_jph_<sfx>` from [jsonplaceholder.openapi.yaml](../../../../test-data/chat-runs-continue/jsonplaceholder.openapi.yaml) with the tools `getPost` and `getUser` | Both toolkits are created; note their ids |
| S2 | Create the agent `autotest_runner_<sfx>` (`POST {{base_url}}/api/v2/elitea_core/applications/prompt_lib/{project_id}`) with the instructions from [r7385-longrunner.instructions.md](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md), the project's default model, reasoning effort low, step limit 25 | The agent is created; note its id and version id. It runs about 45 s with 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`) and answers `RUN-DONE <word>` |
| S3 | Link both toolkits to the agent's version with the tools above (`PATCH {{base_url}}/api/v2/elitea_core/tool/prompt_lib/{project_id}/{toolkit_id}`) | The agent's toolkits list shows both toolkits |
| S4 | Create the conversation `autotest_idle_B_<sfx>` (`POST {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}`) | The conversation is listed in the chat list |

---

## Steps

- Below, **B** is the idle `autotest_idle_B_<sfx>` (no run in it). The new chat of step 1 is created by the test itself.

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click **New chat**, pick `autotest_runner_<sfx>` with `#`, and type the message | The participant button shows `autotest_runner_<sfx>` |
| 2 | Click Send, and click B in the chat list within about 1 s | B opens and the user stays on B |
| 3 | Look at the chat list | The new chat appears with its generated name and the running spinner |
| 4 | Wait for the run to end (about 45 s), then open the new chat | It shows the user message and the answer `RUN-DONE SMK4` |

---

## Expected Final State

The new chat exists with both messages, although the user left it before the first chunk.

---

## Teardown

Always run it, also when a step fails (for example in a `finally` block or a fixture finalizer). A failed delete is logged and doesn't change the verdict.

1. If a run is still going (the test failed midway), stop it first
2. Delete B and the new chat from steps 1–2 (`DELETE {{base_url}}/api/v2/elitea_core/conversation/prompt_lib/{project_id}/{conversation_id}`). Take the new chat's id from its row in step 3; if the test failed before that, find it in `GET {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}?limit=100` as the row created during this run with `autotest_runner_<sfx>` as participant
3. Delete the agent (`DELETE {{base_url}}/api/v2/elitea_core/application/prompt_lib/{project_id}/{agent_id}`)
4. Delete both toolkits (`DELETE {{base_url}}/api/v2/elitea_core/tool/prompt_lib/{project_id}/{toolkit_id}`)
5. Check that none of the entities created by this run is left in the project

---

## Pass/Fail Criteria

**Pass:**
- The new chat is created and listed with a spinner
- The run completes with `RUN-DONE SMK4`

**Fail:**
- The chat isn't created, the user is pulled back to it, or the run is lost

---

## Notes

- **Source functional tests:** ELITEA-4933 (`tests/elitea-platform/chat-interface/chat-runs-continue-in-background/`)
- **Regression rationale:** Leaving right after Send in a brand-new chat races the chat creation, a separate way to fail.
- **Selectors (`data-testid`):** `chat-list-item-running-icon` on the new row
- **Stateless:** each run creates fresh entities and deletes them. Don't reuse a conversation from an earlier run: the agent may reuse the earlier tool results and skip its tools.
- Return to the chat list in-app (New chat → `sidebar-toggle`), never with `page.goto` or a reload: the New response dot is held in the browser only, and a reload drops it.
- Leave the running chat with a real click in the chat list, not a URL change.
- Use the API as the oracle: the conversation (`is_streaming`), `message_traces` for the steps, and `GET {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}?limit=100` for `has_running_task`. Watch the network log for `DELETE .../elitea_core/task/...`.
- Before sending, wait until `chat-switch-participant-button` shows the agent's name. Picking the agent adds it as a participant first and makes it active a moment later; a message sent in between goes to the default assistant, which has no tools.
- The chat URL gets `?name=<conversation name>` appended. Match `/chat/<id>` as a pattern, not the exact URL.
- Stop is an icon-only button next to the composer, with no testid and no `aria-label`. `chat-inject-button` is "Send to the running agent" (a message into the running turn), not Stop.
- After a finished chat is reopened, its steps sit in a collapsed "Thought for …" section (`chat-answer-thought-accordion`, toggle = its inner `button[aria-expanded]`). Expand it before counting steps.
- `message_traces` also returns one `thinking_step` row. Count only the rows with `kind` = `tool_call`.
- To leave before the first chunk, click Send and the chat row in one browser task (for example through `page.evaluate`). Playwright's actionability checks alone can take about 2 s.
