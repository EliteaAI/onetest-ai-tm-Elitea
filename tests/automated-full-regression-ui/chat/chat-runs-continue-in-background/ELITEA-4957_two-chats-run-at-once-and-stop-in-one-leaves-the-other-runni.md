---
id: ELITEA-4957
title: "Two chats run at once and Stop in one leaves the other running"
priority: critical
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

# ELITEA-4957: Two chats run at once and Stop in one leaves the other running

**Module:** chat-interface · **Priority:** critical · **Type:** functional

**Objective:** Runs in different chats are independent: both show the spinner, and Stop in one stops only that run.

---

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- Conversations **A** and **C**, both with R7385LongRunner as the participant, cleared
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

---

## Test Data

| Field | Value |
|-------|-------|
| Message in A | `The word is SMK5A.` |
| Message in C | `The word is SMK5C.` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Send the message in A, open C and send its message | Both rows show the running spinner |
| 2 | In C, wait for the first step and click **Stop** | Exactly one `DELETE /task/...` is sent, for C's run. The Stop button disappears, and C's row gets no dot |
| 3 | Open A | A's run is still going (Stop and "Agent is running…" shown) |
| 4 | Wait for A to end | A's answer is `RUN-DONE SMK5A` |

---

## Expected Final State

C was stopped; A finished normally.

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
- Clear the fixture conversations before each run (`DELETE {{base_url}}/api/v2/elitea_core/messages/prompt_lib/{project_id}/{conversation_id}`). Otherwise the agent may reuse earlier results and skip its tools.
- Return to the chat list in-app (New chat → `sidebar-toggle`), never with `page.goto` or a reload: the New response dot is held in the browser only, and a reload drops it.
- Leave the running chat with a real click in the chat list, not a URL change.
- Use the API as the oracle: the conversation (`is_streaming`), `message_traces` for the steps, and `GET {{base_url}}/api/v2/elitea_core/conversations/prompt_lib/{project_id}?limit=100` for `has_running_task`. Watch the network log for `DELETE .../elitea_core/task/...`.
- Stop must send `DELETE .../elitea_core/task/prompt_lib/{project_id}/{run_uuid}` with C's run uuid only. Take each run uuid from the latest `chat_run_status` "running" socket frame of that chat.
- Related: ELITEA-2621 checks Stop isolation across two tabs or the widget. This case checks it within one tab while switching chats.
