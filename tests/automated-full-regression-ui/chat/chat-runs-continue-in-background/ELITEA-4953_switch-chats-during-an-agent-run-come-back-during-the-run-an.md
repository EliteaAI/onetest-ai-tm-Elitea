---
id: ELITEA-4953
title: "Switch chats during an agent run, come back during the run and after it ends"
priority: critical
type: functional
module: chat-interface
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.chat.test_chat_leave_and_return_running_agent.TestLeaveAndReturnToRunningAgentChat.test_leave_and_return_to_running_agent_chat
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/710b7cf2eee2957a7c24af220a7368f51f685579
tags: [automated:UI:regression, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
known_issues: [elitea_issues#7763]
---

# ELITEA-4953: Switch chats during an agent run, come back during the run and after it ends

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** Leaving a running chat doesn't stop the run, and coming back shows the run live: the steps finished while away, Stop, "Agent is running…", and new steps as they happen.

---

## Preconditions

- User is logged in to `{{base_url}}` and has a project (`{project_id}`). Nothing else is needed: the test creates its own toolkits, agent and conversations in **Setup** and deletes them in **Teardown**. It never uses entities left by other tests or earlier runs. The source files are in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

---

## Test Data

| Field | Value |
|-------|-------|
| Run suffix `<sfx>` | 6 random hex characters, new for every run |
| Message in A | `The word is SMK1.` |

---

## Setup

Every name carries the run suffix `<sfx>` from Test Data, so parallel or repeated runs never meet.

| # | Action | Expected Result |
|---|--------|-----------------|
| S1 | Create two OpenAPI toolkits without credentials (`POST {{base_url}}/api/v2/elitea_core/tools/prompt_lib/{project_id}`): `autotest_echo_<sfx>` from [postman-echo-delay.openapi.yaml](../../../../test-data/chat-runs-continue/postman-echo-delay.openapi.yaml) with the tool `waitSeconds`, and `autotest_jph_<sfx>` from [jsonplaceholder.openapi.yaml](../../../../test-data/chat-runs-continue/jsonplaceholder.openapi.yaml) with the tools `getPost` and `getUser` | Both toolkits are created; note their ids |
| S2 | Create the agent `autotest_runner_<sfx>` (`POST {{base_url}}/api/v2/elitea_core/applications/prompt_lib/{project_id}`) with the instructions from [r7385-longrunner.instructions.md](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md), the project's default model, reasoning effort low, step limit 25 | The agent is created; note its id and version id. It runs about 45 s with 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`) and answers `RUN-DONE <word>` |
| S3 | Link both toolkits to the agent's version with the tools above (`PATCH {{base_url}}/api/v2/elitea_core/tool/prompt_lib/{project_id}/{toolkit_id}`) | The agent's toolkits list shows both toolkits |
| S4 | Create the conversations `autotest_run_A_<sfx>` and `autotest_idle_B_<sfx>` (`POST {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}`), then add the agent as the participant of A (in the UI, or `POST {{base_url}}/api/v2/elitea_core/participants/prompt_lib/{project_id}/{conversation_id}`) | The conversations are listed in the chat list and A has only the agent as participant |

---

## Steps

- Below, **A** is `autotest_run_A_<sfx>` and **B** is the idle `autotest_idle_B_<sfx>` (no run in it).

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, check that the participant button shows `autotest_runner_<sfx>`, then send the message | The run starts and the first tool step appears |
| 2 | After the first step, click B in the chat list | B opens at once. No dialog, and the network log has no `DELETE /task/...` |
| 3 | Look at A's row in the chat list | The row shows the running spinner, labelled "Generating…" |
| 4 | Open A again while the run is still going | A shows the steps that finished while you were away, each with its tool name, plus the Stop button (square icon next to the composer) and "Agent is running…" |
| 5 | Stay in A until the run ends | New steps appear live as they start, the running step has a spinner, and the answer ends with `RUN-DONE SMK1` |
| 6 | Open B, then open A again, and expand "Thought for …" | A shows the final answer and 5 tool steps; no streaming indicator. A's row shows no spinner |
| 7 | Call `GET {{base_url}}/api/v2/elitea_core/message_traces/prompt_lib/{project_id}/{conversation_id}` | 5 `tool_call` traces (plus one `thinking_step`), the same tools in the same order as the UI |

---

## Expected Final State

The run in A finished normally, and the live view after the return matched the server.

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
- The run isn't stopped by leaving
- On return, the finished steps, Stop and "Agent is running…" are shown, and later steps render live
- After the end the UI shows 5 steps = the `tool_call` rows of `message_traces`

**Fail:**
- A dialog appears or `DELETE /task` is sent on leave
- After the return, new steps appear only together with the final answer, or the restored steps have no tool name (known issue #7763)
- The spinner stays in the row after the end

---

## Notes

- **Source functional tests:** ELITEA-4930 (`tests/elitea-platform/chat-interface/chat-runs-continue-in-background/`)
- **Regression rationale:** The core #7385 journey: leaving a running chat must not stop the run, and the returned view must follow it live.
- **Selectors (`data-testid`):** `chat-list-item-running-icon` (row spinner; "Generating…" is its `aria-label`, the hover tooltip may not render headless), `chat-switch-participant-button`, `chat-answer-thought-accordion`
- **Stateless:** each run creates fresh entities and deletes them. Don't reuse a conversation from an earlier run: the agent may reuse the earlier tool results and skip its tools.
- Return to the chat list in-app (New chat → `sidebar-toggle`), never with `page.goto` or a reload: the New response dot is held in the browser only, and a reload drops it.
- Leave the running chat with a real click in the chat list, not a URL change.
- Use the API as the oracle: the conversation (`is_streaming`), `message_traces` for the steps, and `GET {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}?limit=100` for `has_running_task`. Watch the network log for `DELETE .../elitea_core/task/...`.
- Before sending, wait until `chat-switch-participant-button` shows the agent's name. Picking the agent adds it as a participant first and makes it active a moment later; a message sent in between goes to the default assistant, which has no tools.
- The chat URL gets `?name=<conversation name>` appended. Match `/chat/<id>` as a pattern, not the exact URL.
- Stop is an icon-only button next to the composer, with no testid and no `aria-label`. `chat-inject-button` is "Send to the running agent" (a message into the running turn), not Stop.
- After a finished chat is reopened, its steps sit in a collapsed "Thought for …" section (`chat-answer-thought-accordion`, toggle = its inner `button[aria-expanded]`). Expand it before counting steps.
- `message_traces` also returns one `thinking_step` row. Count only the rows with `kind` = `tool_call`.
- Each step row should read "<step>: <tool>". #7763 (open) reports that rows restored after the return lose their tool name and later steps appear only with the final answer. On DEV on 2026-11-27 it did not reproduce (3 runs: late steps rendered live, tool names kept). If it fires, the case fails on steps 4–5.
