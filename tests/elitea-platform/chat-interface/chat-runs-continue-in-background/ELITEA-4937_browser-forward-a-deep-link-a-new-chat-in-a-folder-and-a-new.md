---
id: ELITEA-4937
title: "Browser Forward, a deep link, a new chat in a folder and a new folder during a run"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** Less common ways to leave a running chat (browser Forward, an in-app link, a folder chat, creating a folder) don't stop or block the run.

## Preconditions

- User is logged in to `{{base_url}}`. Create everything below new for this case (no reuse from earlier runs)
- Agent **R7385LongRunner**, imported from [r7385-longrunner.agent.md](../../../../test-data/chat-runs-continue/r7385-longrunner.agent.md) (Agents → **Add agent** → **Import from file**): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- Conversation **A** with R7385LongRunner as the participant
- A chat folder **F**
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `The word is H04.` |
| New folder name | `R7385 tmp <timestamp>` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and wait for the first step | The run is going |
| 2 | Open Artifacts, click browser Back, then browser Forward, then Back | Each happens at once. Forward behaves the same as without a run (do a control without a run if unsure) |
| 3 | In folder F's menu, click **New chat** | An empty chat opens in F with an enabled composer |
| 4 | Create a new folder with the name from Test Data | The folder is created (inline name input + confirm) |
| 5 | Follow an in-app link to the agent page (the participant/agent link) | The agent page opens at once |
| 6 | After the run has ended, open A | `RUN-DONE H04` with 5 steps |

## Expected Final State

The run completed while the user moved through several pages.

## Pass/Fail Criteria

**Pass:**
- No navigation is blocked and none shows "Response generation is still in progress" or "Output is still generating"
- No `DELETE /task`; A ends with 5 steps

**Fail:**
- Any navigation shows a dialog, is blocked, or stops the run

## Teardown

Also after a failed step: stop a run that is still going. Delete the conversations A and the new chat in F, the agent R7385LongRunner and the toolkits `r7385_echo` and `r7385_jph`, then the folders F and `R7385 tmp <timestamp>`.
