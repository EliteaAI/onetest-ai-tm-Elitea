---
id: ELITEA-1306
title: "TTS Active — Other Response Action Bar Controls (Copy, Regenerate, Like/Dislike) Remain Functional"
priority: high
type: functional
module: text-to-speech-tts
status: ready
execution_type: manual
tags: [feature:4500, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4500]
---
# ELITEA-1306: TTS Active — Other Response Action Bar Controls (Copy, Regenerate, Like/Dislike) Remain Functional

**Module:** Text To Speech Tts · **Priority:** High · **Type:** Functional

**Objective:** Verify that other response action bar controls (Copy, Regenerate, Like, Dislike) remain fully functional while TTS playback is active — the presence of the TTS button and active playback must not block or disable other controls.

**Coverage:**
- Copy button works while TTS playing
- Like / Dislike buttons work while TTS playing
- Regenerate button is not blocked by active TTS
- TTS button does not visually obscure other action bar controls

## Preconditions

- Logged in to {{base_url}}
- TTS is configured and enabled
- A Chat session with an AI response is open

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Start TTS playback on an AI response. While audio is playing, click the Copy button on the same response. | Response text is copied to clipboard successfully. TTS playback is unaffected. |
| 2 | While TTS is still playing, click Like or Dislike on the response. | Rating is registered (icon state changes). TTS playback is unaffected. |
| 3 | While TTS is playing, verify the Regenerate button is visible and not greyed out or blocked. | Regenerate button is accessible. (Note: clicking Regenerate should stop TTS per bug EliteaAI/elitea_issues#4995 fix — but the button itself must not be blocked.) |
| 4 | Inspect the response action bar layout while TTS is active. | All buttons are visible, not overlapping each other, and at the correct positions. |

## Expected Final State

All buttons are visible, not overlapping each other, and at the correct positions.

## Pass/Fail Criteria

**Pass:**
- All other action bar controls are accessible and functional during active TTS playback

**Fail:**
- Any action bar control is disabled, hidden, or unresponsive during TTS playback
- TTS button overlaps or obscures another control
