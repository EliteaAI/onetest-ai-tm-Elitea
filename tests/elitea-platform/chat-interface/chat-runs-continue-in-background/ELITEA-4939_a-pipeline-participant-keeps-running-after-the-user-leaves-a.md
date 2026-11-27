---
id: ELITEA-4939
title: "A pipeline participant keeps running after the user leaves and comes back"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, feat:pipelines, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** A pipeline run in chat isn't stopped by leaving, shows as running on return, and ends with the same view as a reload.

## Preconditions

- User is logged in to `{{base_url}}`. Create everything below new for this case (no reuse from earlier runs)
- Pipeline **R7385Pipe**, imported from [r7385-pipe.pipeline.md](../../../../test-data/chat-runs-continue/r7385-pipe.pipeline.md) (Pipelines → **Add pipeline** → **Import from file**): `waitSeconds` 10 → LLM → `waitSeconds` 10 → LLM, answers `PIPE-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385Pipe as the participant
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `The word is H06.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and open B after the first node starts | B opens; no dialog, no `DELETE /task/...` |
| 2 | Open A while the pipeline is still running | The run is shown in progress: Stop and the R7385Pipe node row (a running pipeline shows no "Agent is running…" even in the open chat) |
| 3 | Open B again and come back after the end | The answer `PIPE-DONE H06` and the node steps are shown |
| 4 | Reload the page and open A | The same answer and steps as before the reload |

**Note:** Pipeline `message_traces` are written only when the run ends.

## Expected Final State

The pipeline run completed; the live view matched a reload.

## Pass/Fail Criteria

**Pass:**
- The pipeline isn't stopped by leaving
- On return it shows Stop and the node row
- The end state equals a reload

**Fail:**
- The run is stopped, shown as idle while running, or differs from the reloaded view

## Teardown

Also after a failed step: stop a run that is still going. Delete the conversations A and B, the pipeline R7385Pipe and the toolkit `r7385_echo`.
