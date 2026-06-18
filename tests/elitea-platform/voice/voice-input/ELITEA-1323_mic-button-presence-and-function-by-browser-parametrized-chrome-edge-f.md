---
id: ELITEA-1323
title: "Mic Button Presence and Function by Browser [Parametrized: Chrome | Edge | Firefox]"
priority: critical
type: functional
module: voice-input
status: ready
execution_type: manual
tags: [nfr:accessibility, cross-browser, feature:4499, feat:voice, r-2.0.3, browser]
requirements: [EliteaAI/elitea_issues#4499]
---
# ELITEA-1323: Mic Button Presence and Function by Browser [Parametrized: Chrome | Edge | Firefox]

**Module:** Voice Input · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the microphone button is visible and functional in Chrome, Edge, and Firefox when an ASR model is configured, ensuring cross-browser compatibility of the voice input feature.

**Coverage:**
- Microphone icon visibility in Chrome, Edge, and Firefox with ASR model configured
- Recording start and stop functioning correctly in each browser
- Transcription appearing in the input field in each browser
- Expected behavior in Firefox WITHOUT ASR model: button is hidden (browser Speech API not supported in Firefox)

## Preconditions

- User is logged into ELITEA
- ASR model (gpt-4o-transcribe) configured and active in the project
- Microphone permission granted in the target browser
- Test executed independently in: Chrome, Edge, Firefox
- Chat page open in the target browser

## Test Data

- Parameter: Browser = Chrome | Edge | Firefox
- ASR model: gpt-4o-transcribe
- Test phrase: "Testing microphone functionality"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Chat page in the target browser (Chrome, Edge, or Firefox). Locate the input toolbar. | Microphone icon is present and visible in the input toolbar. |
| 2 | Click the microphone icon. | Recording starts. OS/browser microphone indicator activates. |
| 3 | Speak the phrase "Testing microphone functionality". Pause for ~1 second. | Transcribed text appears in the input field. |
| 4 | Click the microphone icon to stop recording. | Recording stops. Icon returns to inactive state. Transcribed text remains in the input field. |

## Expected Final State

Recording stops. Icon returns to inactive state. Transcribed text remains in the input field.

## Pass/Fail Criteria

**Pass:**
- Microphone button visible and functional in Chrome ✓
- Microphone button visible and functional in Edge ✓
- Microphone button visible and functional in Firefox ✓ (when ASR model is configured)
- Transcription appears correctly in all three browsers

**Fail:**
- Microphone button not visible in any browser with ASR model configured
- Recording fails to start or stop in any browser
- Transcription does not appear in any browser

**Note:** In Firefox WITHOUT an ASR model configured, the button will not appear — this is expected design behavior, not a failure.
