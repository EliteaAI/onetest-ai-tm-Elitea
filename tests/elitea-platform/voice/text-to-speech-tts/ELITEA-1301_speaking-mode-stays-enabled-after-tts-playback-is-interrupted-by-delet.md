---
id: ELITEA-1301
title: "Speaking Mode Stays Enabled After TTS Playback Is Interrupted by Delete or Clear"
priority: high
type: functional
module: text-to-speech-tts
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, feature:, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4995, EliteaAI/elitea_issues#5016]
---
# ELITEA-1301: Speaking Mode Stays Enabled After TTS Playback Is Interrupted by Delete or Clear

**Module:** Text To Speech Tts · **Priority:** High · **Type:** Functional

**Objective:** Verify that when Speaking Mode is active and TTS playback is interrupted by a destructive action (response deletion, chat clear), Speaking Mode itself remains enabled — only the current playback stops, the feature is not toggled off.

**Bug Reference:** EliteaAI/elitea_issues#4995 — notes that Speaking Mode should stay enabled when current read-out is stopped.

**Coverage:**
- Speaking Mode toggle remains ON after playback is stopped by delete or clear
- Speaking Mode continues auto-reading subsequent responses after the interruption
- Speaking Mode is NOT disabled as a side effect of the playback stop

## Preconditions

- Logged in to {{base_url}}
- TTS is configured and enabled
- Speaking Mode is supported and available in the interface
- A Chat session is open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Speaking Mode in the Chat interface | Speaking Mode is ON (toggle/indicator active) |
| 2 | Send a message and wait for an AI response — it should auto-play via Speaking Mode | Audio auto-playback begins for the response |
| 3 | While auto-playback is active, delete the response or clear the chat | Current audio playback stops immediately |
| 4 | Verify the Speaking Mode toggle/indicator state | Speaking Mode remains ON — it was not toggled off by the interruption |
| 5 | Send a new message and wait for the AI response | The new response is automatically read aloud — confirming Speaking Mode is still active and functioning |

## Expected Final State

The new response is automatically read aloud — confirming Speaking Mode is still active and functioning

## Pass/Fail Criteria

**Pass:**
- Speaking Mode toggle/indicator remains ON after delete or clear interrupts playback
- Next AI response is automatically read aloud (Speaking Mode still active)

**Fail:**
- Speaking Mode is toggled OFF after the interruption
- Next AI response is not auto-read (Speaking Mode silently disabled)
