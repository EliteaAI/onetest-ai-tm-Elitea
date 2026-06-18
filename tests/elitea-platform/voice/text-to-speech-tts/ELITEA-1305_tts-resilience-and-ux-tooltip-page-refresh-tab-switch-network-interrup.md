---
id: ELITEA-1305
title: "TTS Resilience and UX — Tooltip, Page Refresh, Tab Switch, Network Interruption, Long Responses, Consistent Design"
priority: medium
type: functional
module: text-to-speech-tts
status: ready
execution_type: manual
tags: [nfr:accessibility, feature:4500, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4500]
---
# ELITEA-1305: TTS Resilience and UX — Tooltip, Page Refresh, Tab Switch, Network Interruption, Long Responses, Consistent Design

**Module:** Text To Speech Tts · **Priority:** Medium · **Type:** Functional

**Objective:** Verify TTS resilience and UX polish — tooltip text, page refresh behavior, browser tab switch behavior, network interruption resilience, long response handling, and consistent visual design across Chat/Agent/Pipeline.

**Coverage:**
- Hovering TTS button shows tooltip "Read out"
- Page refresh during active playback stops playback and releases audio resources (no zombie audio)
- Switching browser tabs during playback does not permanently lock audio output
- Network interruption during playback does not freeze the UI or make Stop unresponsive
- Very long responses (>500 words) play without audio stuttering, choking, or silent gaps
- TTS button visual design (icon, placement) is consistent across Chat, Agent, and Pipeline pages

## Preconditions

- Logged in to {{base_url}}
- TTS is configured and enabled
- Chat, Agent, and Pipeline pages are accessible

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Hover over the TTS read-out button on an AI response (do not click) | Tooltip appears with text 'Read out' |
| 2 | Start TTS playback. While audio is active, refresh the browser page (F5). | Playback stops on refresh. No audio continues after the page reloads. Audio resources are released. |
| 3 | Start TTS playback. Switch to a different browser tab for 10+ seconds, then switch back. | Returning to the tab: audio resumes or was paused gracefully. Audio output is not permanently locked — a new TTS playback can be started. |
| 4 | Start TTS playback on a long response. Simulate a network interruption (disable network for 5 seconds, then re-enable). | UI remains usable during and after the interruption. Stop button remains responsive. No permanent freeze. |
| 5 | Ask the LLM to generate a response of 500+ words. Start TTS playback on the full response. | Audio plays through the full response without stuttering, choking, or unexpected silent gaps. |
| 6 | Navigate to Chat, Agent, and Pipeline pages. Compare the TTS button appearance on each. | Button icon, size, and placement are visually consistent across all three pages. |

## Expected Final State

Button icon, size, and placement are visually consistent across all three pages.

## Pass/Fail Criteria

**Pass:**
- Tooltip "Read out" shown on hover
- Refresh stops playback cleanly
- Tab switch does not permanently lock audio
- Network interruption: UI remains usable; Stop responsive
- Long responses play without stuttering
- Visual design consistent across all three pages

**Fail:**
- Tooltip missing or shows wrong text
- Audio continues after page refresh
- Audio output permanently locked after tab switch
- UI freezes or Stop becomes unresponsive on network drop
- Stuttering or gaps on long responses
