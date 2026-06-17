---
id: ELITEA-1307
title: "TTS Playback Auto-Stops on Response Deletion, Chat Clear, and Regeneration [Bug EliteaAI/elitea_issues#4995, Parametrized: Delete | Clear | Regenerate]"
priority: critical
type: functional
module: text-to-speech-tts
status: ready
execution_type: manual
tags: [feature:4500, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4995, EliteaAI/elitea_issues#4500]
---
# ELITEA-1307: TTS Playback Auto-Stops on Response Deletion, Chat Clear, and Regeneration [Bug EliteaAI/elitea_issues#4995, Parametrized: Delete | Clear | Regenerate]

**Module:** Text To Speech Tts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that active TTS playback automatically stops when the related response is deleted, the chat is cleared, or response regeneration is triggered.

**Bug Reference:** EliteaAI/elitea_issues#4995 — TTS continues reading stale audio even after the response is gone.

**Parameters:**
| # | Action during active TTS playback |
|---|---|
| 1 | Delete the response being read |
| 2 | Clear the entire chat |
| 3 | Start regeneration of the last response |

**Coverage (per parameter):**
- Audio playback stops immediately when the action is performed
- No stale audio continues after the message is removed/replaced
- Behavior is consistent across Chat, Agent, and Pipeline pages

## Preconditions

- Logged in to {{base_url}}
- TTS is configured and enabled
- A Chat session with AI responses is open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| ? | Generate an AI response. Click the TTS read-out button to start playback. | Audio playback begins |
| ? | [Parameter 1] While playback is active, delete the response being read | Playback stops immediately. No audio continues. The deleted message is gone from the UI. |
| ? | [Parameter 2] On a new response, start TTS playback. Then clear the entire chat while audio is playing. | Playback stops immediately. Chat is cleared. No stale audio continues. |
| ? | [Parameter 3] On a new response, start TTS playback. Then click Regenerate while audio is playing. | Playback of the old response stops immediately. Regeneration begins. No old audio continues alongside the new generation. |

## Expected Final State

Playback of the old response stops immediately. Regeneration begins. No old audio continues alongside the new generation.

## Pass/Fail Criteria

**Pass:**
- TTS audio stops immediately for all 3 parameter actions
- No stale audio after message removal/replacement

**Fail:**
- Audio continues after delete, clear, or regeneration
