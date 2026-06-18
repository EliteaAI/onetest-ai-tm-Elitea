---
id: ELITEA-1288
title: "Speaking Mode — Stopping TTS Playback Does Not Disable Speaking Mode"
priority: high
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1288: Speaking Mode — Stopping TTS Playback Does Not Disable Speaking Mode

**Module:** Speaking Mode · **Priority:** High · **Type:** Functional

**Objective:** Verify that manually stopping TTS playback does not disable Speaking Mode — the mode remains ON and voice listening resumes after Stop.

**Coverage:** Stop button halts TTS; Speaking Mode indicator still ON; next voice request works without re-enabling.

## Preconditions

- Speaking Mode active on Chat page; TTS currently playing a response

## Test Data

Request: "Explain quantum computing in detail"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Speaking Mode. Speak: "Explain quantum computing in detail". Auto-send fires → response starts generating; TTS auto-reads. | TTS playing the AI response |
| 2 | While TTS is playing, click the Stop button. | TTS stops immediately |
| 3 | Observe the Speaking Mode indicator in the UI. | Speaking Mode indicator still shows ON |
| 4 | Speak: "Can you summarize that?" | Transcription appears; auto-send fires; AI responds |

## Expected Final State

Transcription appears; auto-send fires; AI responds

## Pass/Fail Criteria

**Pass:**
- Speaking Mode indicator stays ON after Stop; voice listening resumes; next message auto-sends

**Fail:**
- Speaking Mode turns off when Stop is clicked; user must re-enable manually
