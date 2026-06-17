---
id: ELITEA-1292
title: "Speaking Mode — Voice Capture Blocked During TTS After Response Regeneration [Bug #5020]"
priority: high
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5020, EliteaAI/elitea_issues#5016]
---
# ELITEA-1292: Speaking Mode — Voice Capture Blocked During TTS After Response Regeneration [Bug #5020]

**Module:** Speaking Mode · **Priority:** High · **Type:** Functional

**Objective:** Verify voice input is blocked during TTS playback of a regenerated response — same as for the initial response.

**Coverage:** TTS auto-reads regenerated response; voice blocked during this playback; resumes after TTS ends.

## Preconditions

- Speaking Mode active on Chat; at least one exchange exists; speakers functional

## Test Data

Interruption phrase: "But wait, I have another question"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Speaking Mode. Send a message, let TTS finish reading the response. | Full exchange complete |
| 2 | Click Regenerate on the last AI response. Wait for the new response and TTS to start. | TTS auto-reads the regenerated response |
| 3 | While TTS is reading, speak: "But wait, I have another question". | Input field stays empty; no transcription; no auto-send |
| 4 | Let TTS finish. Then speak a new sentence. | Voice capture resumes; transcription appears in input field |

## Expected Final State

Voice capture resumes; transcription appears in input field

## Pass/Fail Criteria

**Pass:**
- Voice blocked during post-regeneration TTS; resumes after it ends

**Fail:**
- Voice captured during TTS playback after regeneration; message auto-sent
