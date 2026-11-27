---
id: ELITEA-4949
title: "The agent editor and test-chat leave dialogs are unchanged"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, feat:agents, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** The change for chat runs doesn't touch the agent page: its unsaved-changes dialog and its test-chat dialogs still appear as before.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- R7385LongRunner opened at `{{base_url}}/app/agents/...?viewMode=owner`
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Unsaved dialog | "There are unsaved changes. Are you sure you want to leave?" (Cancel / Leave) |
| Route change during a test run | "Response generation is still in progress…" (Cancel / Switch) |
| Project switch during a test run | "The agent is being executed. Are you sure you want to leave?" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Change the instructions (don't save) and click Chats in the left menu | The unsaved-changes dialog is shown; Cancel keeps the page |
| 2 | Discard the change. In the test chat, start a run, then click a chat in the left menu | "Response generation is still in progress…" is shown; Cancel keeps the page and the test run keeps going |
| 3 | Switch project with the project selector | "The agent is being executed. Are you sure you want to leave?" is shown; Cancel keeps the page |
| 4 | Stop the test run | Stopped |

## Expected Final State

All three dialogs were shown as before; the user stayed on the page each time.

## Pass/Fail Criteria

**Pass:**
- All three dialogs appear with these texts and Cancel keeps the page

**Fail:**
- A dialog is missing, has another text, or Cancel leaves the page
