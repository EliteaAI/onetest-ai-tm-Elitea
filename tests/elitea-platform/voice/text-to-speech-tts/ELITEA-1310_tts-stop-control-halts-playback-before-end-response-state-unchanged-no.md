---
id: ELITEA-1310
title: "TTS Stop Control — Halts Playback Before End; Response State Unchanged; No Duplicate Audio on Rapid Clicks"
priority: critical
type: functional
module: text-to-speech-tts
status: draft
execution_type: manual
tags: [feature:4500, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4500]
---
# ELITEA-1310: TTS Stop Control — Halts Playback Before End; Response State Unchanged; No Duplicate Audio on Rapid Clicks

**Module:** Text To Speech Tts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that TTS playback can be stopped before it ends, that stopping does not alter the response text or chat state, and that rapidly clicking the read-out button does not produce duplicate or overlapping audio.

**Note:** Pause/Resume is NOT implemented. Only the Stop control is available.

**Coverage:**
- Stop button halts active playback immediately
- Response text and chat state are unaffected after stopping
- No duplicate or overlapping audio streams from rapid clicks

## Preconditions

- Logged in to {{base_url}}
- TTS is configured and enabled
- A Chat session with at least one AI response is open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the TTS read-out button to start audio playback | Audio playback begins and visual indicator is shown |
| 2 | While playback is active, click the Stop button before playback ends naturally | Playback stops immediately. Visual indicator disappears. |
| 3 | Inspect the response text and overall chat state | Response text is unchanged. Chat is not locked, cleared, or altered. All other controls (Copy, Regenerate, etc.) are still accessible. |
| 4 | Rapidly click the TTS read-out button 3–5 times in quick succession | No duplicate or overlapping audio streams. At most one playback session runs at a time. No audio stuttering or unexpected behavior. |

## Expected Final State

No duplicate or overlapping audio streams. At most one playback session runs at a time. No audio stuttering or unexpected behavior.

## Pass/Fail Criteria

**Pass:**
- Stop halts audio immediately; visual indicator clears
- Response text unchanged; chat fully usable after stop
- No audio duplication from rapid clicks

**Fail:**
- Stop button does not halt playback
- Response text altered or chat locked after stop
- Multiple audio streams play simultaneously from rapid clicks
