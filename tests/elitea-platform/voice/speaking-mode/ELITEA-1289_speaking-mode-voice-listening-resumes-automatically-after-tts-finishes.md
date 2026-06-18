---
id: ELITEA-1289
title: "Speaking Mode — Voice Listening Resumes Automatically After TTS Finishes"
priority: high
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1289: Speaking Mode — Voice Listening Resumes Automatically After TTS Finishes

**Module:** Speaking Mode · **Priority:** High · **Type:** Functional

**Objective:** Verify that voice listening automatically resumes after TTS finishes playing, allowing the next request without any manual re-activation.

**Coverage:** TTS completes → voice re-activates → second request transcribed and auto-sent.

## Preconditions

- Speaking Mode active on Chat page; speakers/headphones functional

## Test Data

Request 1: "What is photosynthesis?" | Request 2: "Give me a short example"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Speaking Mode. Speak Request 1: "What is photosynthesis?" → auto-send fires. Let TTS read the response to completion. | Response received; TTS plays fully and stops |
| 2 | Wait 2–3 seconds after TTS finishes, then speak Request 2: "Give me a short example". | Transcription appears in input; auto-send fires; second AI response received |

## Expected Final State

Transcription appears in input; auto-send fires; second AI response received

## Pass/Fail Criteria

**Pass:**
- Voice listening resumes automatically after TTS ends; second request transcribed and sent without any button click

**Fail:**
- Voice does not resume after TTS; user must re-enable Speaking Mode manually
