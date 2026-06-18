---
id: ELITEA-1303
title: "TTS — Stop and Re-trigger Restarts Playback from Beginning; Button Keyboard Accessible (Tab + Enter/Space)"
priority: high
type: functional
module: text-to-speech-tts
status: ready
execution_type: manual
tags: [nfr:accessibility, feature:4500, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4500]
---
# ELITEA-1303: TTS — Stop and Re-trigger Restarts Playback from Beginning; Button Keyboard Accessible (Tab + Enter/Space)

**Module:** Text To Speech Tts · **Priority:** High · **Type:** Functional

**Objective:** Verify that stopping TTS playback mid-way and re-triggering it restarts from the beginning of the response (not from where it stopped), and that the TTS button is fully keyboard accessible via Tab + Enter/Space.

**Coverage:**
- Re-triggering TTS after stop restarts from the beginning
- TTS button focusable via Tab key
- TTS button activatable via Enter or Space
- Stop button focusable and activatable via keyboard

## Preconditions

- Logged in to {{base_url}}
- TTS is configured and enabled
- A Chat session with an AI response is open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the TTS read-out button to start playback. Wait a few seconds into the response, then click Stop. | Playback stops mid-way |
| 2 | Click the TTS read-out button again on the same response | Playback restarts from the beginning of the response, not from where it was stopped |
| 3 | Use Tab key to navigate the response action bar and focus on the TTS button | TTS button receives keyboard focus (visible focus ring) |
| 4 | Press Enter or Space while the TTS button is focused | TTS playback starts |
| 5 | Tab to the Stop button and press Space or Enter | Playback stops |

## Expected Final State

Playback stops

## Pass/Fail Criteria

**Pass:**
- Re-trigger after stop plays from the beginning (not mid-point)
- Keyboard navigation reaches TTS button
- Enter/Space starts and stops playback

**Fail:**
- Re-trigger continues from where it stopped (resume behavior not expected)
- TTS button unreachable via keyboard
- Enter/Space has no effect on the TTS button
