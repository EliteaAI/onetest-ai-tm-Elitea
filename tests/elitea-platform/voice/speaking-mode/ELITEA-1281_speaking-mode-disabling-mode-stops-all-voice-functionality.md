---
id: ELITEA-1281
title: "Speaking Mode — Disabling Mode Stops All Voice Functionality"
priority: critical
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1281: Speaking Mode — Disabling Mode Stops All Voice Functionality

**Module:** Speaking Mode · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that disabling Speaking Mode fully stops all associated functionality — voice is no longer captured, no auto-read occurs, the Send button is restored, and no background microphone session remains active.

**Coverage:** Toggle OFF → mic stops capturing → Send button restored → TTS does not auto-read → no orphaned mic session.

## Preconditions

- Speaking Mode is currently active on Chat page; mic permission granted; at least one prior exchange in chat

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm Speaking Mode is ON: Speaking Mode button visible (replacing Send), mic active. | Speaking Mode active; Send button replaced by Speaking Mode button |
| 2 | Click the Speaking Mode button to disable it. | Speaking Mode turns OFF; standard Send button reappears in the input area |
| 3 | Speak a sentence clearly into the mic. | No transcription appears in the input field; voice is not captured or cached |
| 4 | Type a message manually and click Send. | Message sends normally; AI responds; TTS does NOT auto-read the response |
| 5 | Open browser DevTools → check active microphone/audio streams (Application or Network tab). | No active mic stream or orphaned WebSocket/SSE session from Speaking Mode |

## Expected Final State

No active mic stream or orphaned WebSocket/SSE session from Speaking Mode

## Pass/Fail Criteria

**Pass:**
- Send button restored after disable
- Spoken words not transcribed or captured after disable
- TTS does not auto-read AI response
- No background mic session or orphaned connection remains

**Fail:**
- Voice still transcribed after Speaking Mode disabled
- TTS still auto-reads responses
- Send button not restored
- Background mic stream remains active
