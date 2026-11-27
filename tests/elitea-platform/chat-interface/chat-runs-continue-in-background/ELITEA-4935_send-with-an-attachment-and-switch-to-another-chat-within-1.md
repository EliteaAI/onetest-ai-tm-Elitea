---
id: ELITEA-4935
title: "Send with an attachment and switch to another chat within 1 second"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, feat:attachments, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** A send that carries an attachment completes when the user switches away within a second of clicking Send.

## Preconditions

- User is logged in to `{{base_url}}`. Create everything below new for this case (no reuse from earlier runs)
- Agent **R7385LongRunner**, imported from [r7385-longrunner.agent.md](../../../../test-data/chat-runs-continue/r7385-longrunner.agent.md) (Agents → **Add agent** → **Import from file**): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385LongRunner as the participant
- A text file `r7385.txt` with one word inside
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `Read the file, the word is H01.` |
| File | `r7385.txt` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, attach `r7385.txt` and type the message | The attachment chip is shown in the composer |
| 2 | Click Send and click B within 1 s, before any answer chunk | B opens; no dialog, no `DELETE /task/...` |
| 3 | Wait on B until the run ends (A's row stops spinning), then open A | The user message has the attachment chip, and the answer ends with `RUN-DONE H01` |
| 4 | Call `GET {{base_url}}/api/v2/elitea_core/conversation/prompt_lib/{project_id}/{conversation_id}` | One new message group; it was streaming and is now `is_streaming: false` |

## Expected Final State

The message with its attachment was sent and answered although the user left at once.

## Pass/Fail Criteria

**Pass:**
- The attachment is kept on the user message
- The run completes

**Fail:**
- The send is lost, the attachment is lost, or the run is stopped

## Teardown

Also after a failed step: stop a run that is still going. Delete the conversations A and B, the agent R7385LongRunner and the toolkits `r7385_echo` and `r7385_jph`.
