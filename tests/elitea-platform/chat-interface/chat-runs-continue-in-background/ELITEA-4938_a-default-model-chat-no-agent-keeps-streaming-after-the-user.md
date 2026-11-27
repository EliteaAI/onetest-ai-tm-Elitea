---
id: ELITEA-4938
title: "A default-model chat (no agent) keeps streaming after the user leaves and comes back"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, r-2.0.9]
requirements: [EliteaAI/elitea_issues#7385]
---

**Objective:** A plain chat with no agent participant keeps generating while the user is away, and on return the answer keeps growing live.

## Preconditions

- User is logged in to `{{base_url}}`. Create everything below new for this case (no reuse from earlier runs)
- An idle conversation **B** (no run in it) to switch to
- Conversation **A** with no participant
- In the composer, pick a model that writes long lists (for example Claude Haiku). If the project's default model loads skills that refuse long lists, pick another model
- DevTools → Network is open to watch for `DELETE .../elitea_core/task/...` requests

## Test Data

| Field | Value |
|-------|-------|
| Message | `Write a numbered list of 600 short lines about numbers, then the line TEXT-DONE H05.` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | In A, send the message and wait for the first answer text | Text streams |
| 2 | Open B, wait a few seconds, then open A while the server still shows the group streaming | Stop and the streaming indicator are shown |
| 3 | Watch A for 10 s | The answer keeps growing live (the line count increases several times) |
| 4 | After the end, open B and come back to A | The full answer ends with `TEXT-DONE H05`; no streaming indicator |
| 5 | Compare the UI text with the conversation API | The same text |

## Expected Final State

The plain chat finished its answer while the user was away and back.

## Pass/Fail Criteria

**Pass:**
- No dialog, no `DELETE /task`
- The answer grows live after the return
- The final text equals the server text

**Fail:**
- Text written after the return appears only at the end, or the final text differs from the server

## Teardown

Also after a failed step: stop a run that is still going. Delete the conversations A and B.
