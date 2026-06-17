---
id: ELITEA-1311
title: "TTS Core Smoke — Button Visible, Playback Triggers, Only Final Answer Spoken, Visual Indicator Auto-Clears"
priority: critical
type: functional
module: text-to-speech-tts
status: ready
execution_type: manual
tags: [feature:4500, feat:voice, r-2.0.3, smoke]
requirements: [EliteaAI/elitea_issues#4500]
---
# ELITEA-1311: TTS Core Smoke — Button Visible, Playback Triggers, Only Final Answer Spoken, Visual Indicator Auto-Clears

**Module:** Text To Speech Tts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the TTS core happy path — the read-out button is visible in the Chat response action bar, clicking it triggers audio playback of only the final AI answer (thinking steps excluded), a visual indicator is active during playback, and everything resets automatically when playback finishes.

**Note:** Pause/Resume is NOT implemented. Only the Stop control is available.

**Coverage:**
- TTS button visible in the response action bar
- Clicking the button triggers audio playback
- Only the final AI answer is read — thinking steps and internal reasoning are not spoken
- Visual indicator (animation/icon state change) is shown during active playback
- Indicator disappears and button resets to default state when playback ends naturally

## Preconditions

- Logged in to {{base_url}}
- TTS is enabled (TTS model configured in project Integrations → Speech Synthesis)
- A Chat session is open
- At least one AI response has been received

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Send a message in Chat and wait for an AI response (ideally one where thinking steps are visible) | AI response is displayed. A TTS read-out button is visible in the response action bar. |
| 2 | Click the TTS read-out button on the response | Audio playback begins. Only the final AI answer is read aloud — thinking steps and internal processing output are silent. |
| 3 | While playback is active, observe the visual indicator | A visual indicator (animation, icon state change) is clearly shown on the TTS button or response action bar. |
| 4 | Wait for playback to finish naturally without stopping it | Playback completes. The visual indicator disappears. The TTS button returns to its default (non-active) state. |

## Expected Final State

Playback completes. The visual indicator disappears. The TTS button returns to its default (non-active) state.

## Pass/Fail Criteria

**Pass:**
- TTS button visible in response action bar
- Audio plays the final AI answer only (thinking steps silent)
- Visual indicator active during playback, clears when done

**Fail:**
- Button missing or hidden
- Thinking steps are read aloud
- No visual indicator, or indicator persists after playback ends
