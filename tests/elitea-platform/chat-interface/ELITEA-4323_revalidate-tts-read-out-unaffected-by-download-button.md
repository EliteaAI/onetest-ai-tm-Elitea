---
id: ELITEA-4323
title: "Download Button Does Not Interfere With Read Out (TTS) Behavior"
priority: high
type: regression
module: chat-interface
status: draft
execution_type: manual
tags: [feat:chat, feat:voice, comm:feedback, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7144]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Release/2.0.8 build (containing the chat code-block download feature) is deployed to the test environment
- A chat conversation exists with an AI response containing both prose text and a fenced code block
- This is a regression re-check of ELITEA-1302 (TTS Read Out button available and functional) and ELITEA-1309 (TTS Read Out file/image chips not read as "object object"), triggered by the new Download icon added to the code block toolbar

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/chat` |
| Prompt | "Explain what a REST API is and give a short json example" |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to `{{base_url}}/app/chat`, open or create a conversation, and send the Test Data prompt | AI responds with a message containing prose text and a fenced json code block with Edit code/Copy code/Download in its toolbar |
| 2 | Re-run ELITEA-1302: click the Read Out (TTS) button on the AI response | TTS playback starts and reads the message content aloud, exactly as before the Download icon was introduced |
| 3 | While TTS is reading, click the Download icon on the code block | File downloads successfully; TTS playback is not interrupted, corrupted, or caused to error by the Download action |
| 4 | Allow TTS playback to reach the portion of the message containing the code block | Re-run ELITEA-1309 expectation: the code block content is either skipped appropriately or read in a sensible way, not read as "object object" or similar artifact caused by the new Download icon/toolbar markup |
| 5 | Stop TTS playback and click Read Out again on the same message | TTS restarts correctly; no stuck state or control conflict with the Download icon |

## Expected Final State

TTS Read Out continues to function exactly as before the Download icon was introduced, with no interruption, corruption, or "object object" artifact traceable to the new toolbar control.

## Pass/Fail Criteria

**Pass:**
- Read Out button starts/stops TTS playback normally with the Download icon present
- Clicking Download during TTS playback does not interrupt or break playback
- No "object object" or similar read-aloud artifact is introduced near the code block

**Fail:**
- Read Out button is missing, broken, or behaves differently due to the new Download icon
- TTS playback is interrupted, errors, or gets stuck when Download is clicked
- TTS reads a corrupted/artifact string (e.g. "object object") near the code block/toolbar area
