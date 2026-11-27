---
id: ELITEA-4956
title: "Send in a new chat and switch to another chat at once"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

# ELITEA-4956: Send in a new chat and switch to another chat at once

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** Switching away right after Send in a brand-new chat (before the first chunk) still creates the chat and completes the run.

---

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

---

## Test Data

| Field | Value |
|-------|-------|
| Message | `#R7385LongRunner The word is SMK4.` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Click **New chat**, pick R7385LongRunner with `#`, and type the message | The participant button shows R7385LongRunner |
| 2 | Click Send, and click B in the chat list within about 1 s | B opens and the user stays on B |
| 3 | Look at the chat list | The new chat appears with its generated name and the running spinner |
| 4 | Wait for the run to end (about 45 s), then open the new chat | It shows the user message and the answer `RUN-DONE SMK4` |

---

## Expected Final State

The new chat exists with both messages, although the user left it before the first chunk.

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
- Clear the fixture conversations before each run (`DELETE {{base_url}}/api/v2/elitea_core/messages/prompt_lib/{project_id}/{conversation_id}`). Otherwise the agent may reuse earlier results and skip its tools.
- Return to the chat list in-app (New chat → `sidebar-toggle`), never with `page.goto` or a reload: the New response dot is held in the browser only, and a reload drops it.
- Leave the running chat with a real click in the chat list, not a URL change.
- Use the API as the oracle: the conversation (`is_streaming`), `message_traces` for the steps, and `GET {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}?limit=100` for `has_running_task`. Watch the network log for `DELETE .../elitea_core/task/...`.
- Before sending, wait until `chat-switch-participant-button` shows the agent's name. Picking the agent adds it as a participant first and makes it active a moment later; a message sent in between goes to the default assistant, which has no tools.
- The chat URL gets `?name=<conversation name>` appended. Match `/chat/<id>` as a pattern, not the exact URL.
- Stop is an icon-only button next to the composer, with no testid and no `aria-label`. `chat-inject-button` is "Send to the running agent" (a message into the running turn), not Stop.
- After a finished chat is reopened, its steps sit in a collapsed "Thought for …" section (`chat-answer-thought-accordion`, toggle = its inner `button[aria-expanded]`). Expand it before counting steps.
- `message_traces` also returns one `thinking_step` row. Count only the rows with `kind` = `tool_call`.
- To leave before the first chunk, click Send and the chat row in one browser task (for example through `page.evaluate`). Playwright's actionability checks alone can take about 2 s.
- Delete the created conversation at the end.
