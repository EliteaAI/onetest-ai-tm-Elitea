---
id: ELITEA-4951
title: "A second tab of the same user shows the spinner and the New response dot"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** Run indicators reach the user's other open tab.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385LongRunner as the participant, cleared
- Two browser tabs: tab 1 on A, tab 2 on B
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `The word is M09.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In tab 1, send the message in A | The run starts |
| 2 | Look at A's row in tab 2 | The spinner shows within 2 s of the start |
| 3 | Wait for the end | Tab 2 shows the "New response" dot on A's row |

## Expected Final State

Tab 2 followed the run started in tab 1.

## Pass/Fail Criteria

**Pass:**
- Spinner within 2 s and the dot after the end in tab 2

**Fail:**
- Tab 2 shows nothing, or only after a reload
