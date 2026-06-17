---
id: ELITEA-1325
title: "Voice Input — Core Smoke Test (Chat, Agent, and Pipeline Pages)"
priority: critical
type: functional
module: voice-input
status: ready
execution_type: manual
tags: [nfr:accessibility, feature:4499, feat:voice, r-2.0.3, smoke]
requirements: [EliteaAI/elitea_issues#4499]
---
# ELITEA-1325: Voice Input — Core Smoke Test (Chat, Agent, and Pipeline Pages)

**Module:** Voice Input · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the voice input feature works end-to-end on Chat, Agent, and Pipeline pages — from microphone activation through transcription to message submission.

**Coverage:**
- Microphone icon visibility and placement without overlapping other toolbar controls
- Recording start: OS/browser mic indicator activates; icon switches to active state; input border shows recording glow
- Transcription appears in the input field sentence by sentence after each pause
- Recording stop: icon returns to inactive state; no further transcription occurs
- Message submission via Send button and via Enter key
- Feature works consistently across Chat, Agent, and Pipeline pages

## Preconditions

- User is logged into ELITEA ({{base_url}})
- An ASR model (gpt-4o-transcribe preferred) is configured and active in the project settings under Integrations → Speech Recognition (ASR)
- Microphone permission is granted for the ELITEA domain in the browser
- At least one conversation exists on the Chat page
- Browser: Chrome or Edge

## Test Data

- ASR model name: gpt-4o-transcribe (any non-Whisper ASR model)
- Test phrase: "Hello, this is a voice input test"
- Target pages: Chat, Agent, Pipeline

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Chat page. Locate the microphone icon in the chat input toolbar. | Microphone icon is visible and does not overlap other toolbar controls (Send button, attachment button, etc.). |
| 2 | Click the microphone icon. | The OS/browser microphone indicator activates. The microphone icon changes to its active/recording appearance. The input field border changes to a primary-color glow. |
| 3 | Speak the phrase "Hello, this is a voice input test." Pause for approximately 1 second. | Transcribed text appears in the input field after the pause. Text is appended sentence by sentence. |
| 4 | Click the microphone icon again to stop recording. | The microphone icon returns to its inactive appearance. The input field border returns to default. No further transcription occurs. |
| 5 | Click the Send button to submit the transcribed message. | The message is sent successfully. An AI response appears below the submitted message. |
| 6 | Start a new recording, speak a new phrase, stop, then submit using the Enter key. | The message is submitted and processed identically to using the Send button. |
| 7 | Navigate to the Agent page. Repeat steps 2–5 in the Agent chat input. | Microphone icon is present and functional. Full recording and submission flow completes without errors. |
| 8 | Navigate to the Pipeline page. Repeat steps 2–5 in the Pipeline chat input. | Microphone icon is present and functional. Full recording and submission flow completes without errors. |

## Expected Final State

Microphone icon is present and functional. Full recording and submission flow completes without errors.

## Pass/Fail Criteria

**Pass:**
- Microphone icon visible on all three pages without layout issues
- Recording starts, transcription appears, and recording stops correctly on all three pages
- Transcribed text is successfully submitted and produces an AI response on all three pages

**Fail:**
- Microphone icon missing, hidden, or overlapping other controls on any page
- Recording fails to start or stop correctly on any page
- Transcription does not appear or appears incorrectly
- Message submission fails after voice input on any page
