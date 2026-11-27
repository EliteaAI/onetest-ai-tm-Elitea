---
id: ELITEA-4943
title: "Switching project during a run doesn't stop it"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** A chat run keeps going when the user switches to another project and back.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- Conversation **A** with R7385LongRunner as the participant, cleared
- The user has access to a second project **P2**
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `The word is M01.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and wait for the first step | The run is going |
| 2 | Switch to P2 with the project selector | P2 opens; no dialog, no `DELETE /task/...` |
| 3 | Wait a few seconds and switch back to the first project, then open A | A shows the run (in progress or ended) |
| 4 | Wait for the end | `RUN-DONE M01` with 5 steps |

## Expected Final State

The run completed across the project switch.

## Pass/Fail Criteria

**Pass:**
- The run isn't stopped by the project switch

**Fail:**
- A dialog appears, or the run is stopped
