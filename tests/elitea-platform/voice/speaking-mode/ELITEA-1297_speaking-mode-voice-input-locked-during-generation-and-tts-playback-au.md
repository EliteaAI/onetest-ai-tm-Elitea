---
id: ELITEA-1297
title: "Speaking Mode — Voice Input Locked During Generation and TTS Playback (Auto-Read and Manual Read Out)"
priority: critical
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1297: Speaking Mode — Voice Input Locked During Generation and TTS Playback (Auto-Read and Manual Read Out)

**Module:** Speaking Mode · **Priority:** Critical · **Type:** Functional

**Objective:** Verify voice capture is blocked in all three states: (1) while AI is generating a response, (2) while TTS is auto-reading it aloud, and (3) while the user manually triggers "Read Out" on any response. Voice resumes only after each state ends or is stopped.

**Coverage:** No transcription or auto-send during generation, auto-TTS read, or manual Read Out; voice resumes after each ends.

## Preconditions

- Speaking Mode active on Chat page; existing conversation; mic permission granted; speakers/headphones functional

## Test Data

Request: "Explain the history of the internet" | Interruption phrase: "Are you still listening?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Speaking Mode. Speak: "Explain the history of the internet". Let it auto-send. | Message sent; AI starts generating (spinner visible) |
| 2 | While AI is generating, speak: "Are you still listening?" | Input field stays empty; no transcription during generation |
| 3 | Wait for full response. Observe TTS auto-read starting. While TTS plays, speak: "Are you still listening?" | Input field stays empty; no transcription during auto-TTS read |
| 4 | Let TTS finish. Then speak a new sentence. | Transcription now appears; voice is active again |
| 5 | Scroll to an earlier response. Click its "Read Out" button manually. While it plays, speak: "Are you still listening?" | Input field stays empty during manual Read Out |
| 6 | Click Stop on the manual Read Out. Then speak a sentence. | Voice capture resumes; transcription appears in input field |

## Expected Final State

Voice capture resumes; transcription appears in input field

## Pass/Fail Criteria

**Pass:**
- No voice captured during generation, auto-TTS, or manual Read Out
- Voice resumes correctly after each blocked state ends

**Fail:**
- Transcription appears or a message is sent during any of the blocked states
