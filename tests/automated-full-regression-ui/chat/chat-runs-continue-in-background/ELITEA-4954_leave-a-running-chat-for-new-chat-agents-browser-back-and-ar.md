---
id: ELITEA-4954
title: "Leave a running chat for New chat, Agents, browser Back and Artifacts, then see the New response dot"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

# ELITEA-4954: Leave a running chat for New chat, Agents, browser Back and Artifacts, then see the New response dot

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** Every way of leaving a running chat (New chat, left menu, browser Back, Artifacts) keeps the run going, and a run that ends while you are away marks its row with the New response dot.

---

## Preconditions

- User is logged in to `{{base_url}}` and has a project (`{project_id}`). Nothing else is needed: the test creates its own toolkits, agent and conversations in **Setup** and deletes them in **Teardown**. It never uses entities left by other tests or earlier runs. The source files are in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

---

## Test Data

| Field | Value |
|-------|-------|
| Run suffix `<sfx>` | 6 random hex characters, new for every run |
| Message in A | `The word is SMK2.` |

---

## Setup

Every name carries the run suffix `<sfx>` from Test Data, so parallel or repeated runs never meet.

| # | Action | Expected Result |
|---|--------|-----------------|
| S1 | Create two OpenAPI toolkits without credentials (`POST {{base_url}}/api/v2/elitea_core/tools/prompt_lib/{project_id}`): `autotest_echo_<sfx>` from [postman-echo-delay.openapi.yaml](../../../../test-data/chat-runs-continue/postman-echo-delay.openapi.yaml) with the tool `waitSeconds`, and `autotest_jph_<sfx>` from [jsonplaceholder.openapi.yaml](../../../../test-data/chat-runs-continue/jsonplaceholder.openapi.yaml) with the tools `getPost` and `getUser` | Both toolkits are created; note their ids |
| S2 | Create the agent `autotest_runner_<sfx>` (`POST {{base_url}}/api/v2/elitea_core/applications/prompt_lib/{project_id}`) with the instructions from [r7385-longrunner.instructions.md](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md), the project's default model, reasoning effort low, step limit 25 | The agent is created; note its id and version id. It runs about 45 s with 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`) and answers `RUN-DONE <word>` |
| S3 | Link both toolkits to the agent's version with the tools above (`PATCH {{base_url}}/api/v2/elitea_core/tool/prompt_lib/{project_id}/{toolkit_id}`) | The agent's toolkits list shows both toolkits |
| S4 | Create the conversation `autotest_run_A_<sfx>` (`POST {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}`), then add the agent as the participant of A (in the UI, or `POST {{base_url}}/api/v2/elitea_core/participants/prompt_lib/{project_id}/{conversation_id}`) | The conversation is listed in the chat list and A has only the agent as participant |

---

## Steps

- Below, **A** is `autotest_run_A_<sfx>`.

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and wait for the first step | The run is going |
| 2 | Click **New chat** | An empty chat opens at once and its composer is enabled |
| 3 | Open **Agents** in the left menu | The Agents page opens at once |
| 4 | Click the browser Back button, then open **Artifacts** | Each page opens at once. No "Response generation is still in progress…" dialog and no "Output is still generating" text anywhere |
| 5 | Stay away until the run has ended (about 45 s from the send), then open the chat list in-app (New chat → chat list) | A's row shows the dot with the tooltip "New response" |
| 6 | Open A and expand "Thought for …" | The answer `RUN-DONE SMK2` and all 5 steps are shown; no streaming indicator. The dot is gone and stays gone |

---

## Expected Final State

The run finished while the user was on other pages, and the row marked the new answer until it was opened.

---

## Teardown

Always run it, also when a step fails (for example in a `finally` block or a fixture finalizer). A failed delete is logged and doesn't change the verdict.

1. If a run is still going (the test failed midway), stop it first
2. Delete the conversation A (`DELETE {{base_url}}/api/v2/elitea_core/conversation/prompt_lib/{project_id}/{conversation_id}`)
3. Delete the agent (`DELETE {{base_url}}/api/v2/elitea_core/application/prompt_lib/{project_id}/{agent_id}`)
4. Delete both toolkits (`DELETE {{base_url}}/api/v2/elitea_core/tool/prompt_lib/{project_id}/{toolkit_id}`)
5. Check that none of the entities created by this run is left in the project

---

## Pass/Fail Criteria

**Pass:**
- No dialog and no `DELETE /task` for any of the four navigations
- The New response dot appears after the end and clears on open
- A shows the full answer and 5 steps

**Fail:**
- Any navigation shows a dialog, is delayed, or stops the run
- No dot, or the dot stays after A is opened

---

## Notes

- **Source functional tests:** ELITEA-4931 (`tests/elitea-platform/chat-interface/chat-runs-continue-in-background/`)
- **Regression rationale:** Every way out of a running chat, plus the dot that is only shown when a run ends while the user is away.
- **Selectors (`data-testid`):** `chat-list-item-unread-badge` with `data-reason=new_response` (tooltip "New response")
- **Stateless:** each run creates fresh entities and deletes them. Don't reuse a conversation from an earlier run: the agent may reuse the earlier tool results and skip its tools.
- Return to the chat list in-app (New chat → `sidebar-toggle`), never with `page.goto` or a reload: the New response dot is held in the browser only, and a reload drops it.
- Leave the running chat with a real click in the chat list, not a URL change.
- Use the API as the oracle: the conversation (`is_streaming`), `message_traces` for the steps, and `GET {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}?limit=100` for `has_running_task`. Watch the network log for `DELETE .../elitea_core/task/...`.
- Before sending, wait until `chat-switch-participant-button` shows the agent's name. Picking the agent adds it as a participant first and makes it active a moment later; a message sent in between goes to the default assistant, which has no tools.
- The chat URL gets `?name=<conversation name>` appended. Match `/chat/<id>` as a pattern, not the exact URL.
- Stop is an icon-only button next to the composer, with no testid and no `aria-label`. `chat-inject-button` is "Send to the running agent" (a message into the running turn), not Stop.
- After a finished chat is reopened, its steps sit in a collapsed "Thought for …" section (`chat-answer-thought-accordion`, toggle = its inner `button[aria-expanded]`). Expand it before counting steps.
- `message_traces` also returns one `thinking_step` row. Count only the rows with `kind` = `tool_call`.
- Assert that the texts "Response generation is still in progress" and "Output is still generating" never appear, and that no native `beforeunload` dialog opens (record `page.on('dialog')`).
- Come back to the chat list in-app. A page reload drops the New response dot, because it is held in the browser only.
