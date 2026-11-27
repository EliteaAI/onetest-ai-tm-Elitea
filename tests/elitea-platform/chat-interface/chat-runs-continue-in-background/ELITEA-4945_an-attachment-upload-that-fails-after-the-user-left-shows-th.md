---
id: ELITEA-4945
title: "An attachment upload that fails after the user left shows the same error on return"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, feat:attachments, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** If a send fails (attachment upload error) after the user switched away, the error isn't lost and no run is left hanging.

## Preconditions

- User is logged in to `{{base_url}}` and has a project with the fixtures below. Fixtures are described in [test-data/chat-runs-continue](../../../../test-data/chat-runs-continue/README.md)
- Agent **R7385LongRunner** ([instructions](../../../../test-data/chat-runs-continue/r7385-longrunner.instructions.md)): about 45 s, 5 tool calls (`waitSeconds` 10 s ×3, `getPost`, `getUser`), answers `RUN-DONE <word>`
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with R7385LongRunner as the participant, cleared
- A way to make the attachment upload fail, for example DevTools → Network request blocking for the attachments upload URL (`.../elitea_core/attachments/...`)
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Error text | "Failed to upload attachments, please try again." |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Control: with uploads blocked, attach a file in A, send, and stay | Note the error text and where it is shown |
| 2 | Repeat: attach a file, send, and click B within 1 s | B opens |
| 3 | Open A again | The same error is shown in the same place as in the control |
| 4 | Look at A's row and the chat | No spinner, no "Agent is running…"; the server has no new message group |

**Note:** The attachment chip is also lost on a plain chat switch with a draft. That is existing draft behaviour and isn't checked here.

## Expected Final State

The failure was reported on return and nothing is left running. Unblock the upload URL.

## Pass/Fail Criteria

**Pass:**
- The error on return equals the control
- No orphan running state

**Fail:**
- The error is lost, or the chat or row shows a run that doesn't exist
