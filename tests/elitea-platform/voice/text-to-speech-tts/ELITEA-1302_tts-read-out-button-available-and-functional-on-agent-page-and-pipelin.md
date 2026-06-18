---
id: ELITEA-1302
title: "TTS Read Out Button Available and Functional on Agent Page and Pipeline Page"
priority: high
type: functional
module: text-to-speech-tts
status: ready
execution_type: manual
tags: [feature:4500, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4500]
---
# ELITEA-1302: TTS Read Out Button Available and Functional on Agent Page and Pipeline Page

**Module:** Text To Speech Tts · **Priority:** High · **Type:** Functional

**Objective:** Verify that the TTS "Read out" button is present and functional on Agent and Pipeline execution pages — not only in the Chat interface.

**Coverage:**
- TTS button visible in the response action bar on the Agent page (Test Settings)
- TTS button visible in the response action bar on the Pipeline page
- Clicking the button triggers audio playback on both pages
- Stop control works on both pages
- Visual indicator behaves correctly on both pages

## Preconditions

- Logged in to {{base_url}}
- TTS is configured and enabled
- An agent with Test Settings access is available
- A pipeline that produces a chat response is available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent page and open an agent's Test Settings panel. Send a request and wait for the AI response. | AI response is shown. TTS read-out button is visible in the response action bar. |
| 2 | Click the TTS button on the Agent page response. While playing, click Stop. | Audio playback starts. Stop halts it. Visual indicator behaves correctly. |
| 3 | Navigate to the Pipeline page. Run a pipeline and wait for the chat response in the run output. | Pipeline produces a response. TTS read-out button is visible in the response action bar. |
| 4 | Click the TTS button on the Pipeline page response. While playing, click Stop. | Audio playback starts. Stop halts it. Visual indicator behaves correctly. |

## Expected Final State

Audio playback starts. Stop halts it. Visual indicator behaves correctly.

## Pass/Fail Criteria

**Pass:**
- TTS button present and functional on Agent and Pipeline pages
- Audio plays and stops correctly on both surfaces

**Fail:**
- TTS button missing on Agent page or Pipeline page
- Button present but non-functional on either page
