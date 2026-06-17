---
id: ELITEA-1291
title: "Speaking Mode — Auto-Send Not Triggered by Natural Mid-Sentence Pauses [Bug #5028]"
priority: high
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5028, EliteaAI/elitea_issues#5016]
---
# ELITEA-1291: Speaking Mode — Auto-Send Not Triggered by Natural Mid-Sentence Pauses [Bug #5028]

**Module:** Speaking Mode · **Priority:** High · **Type:** Functional

**Objective:** Verify auto-send does not fire during natural pauses between sentences — only after the user fully stops speaking.

**Coverage:** Mid-sentence pause (~2 sec) does not trigger send; both sentences combine into one message; send fires after full stop.

## Preconditions

- Speaking Mode active on Chat; quiet test environment

## Test Data

Sentence 1: "Tell me about the history of computers." [~2 sec pause] Sentence 2: "And include milestones from 1950 onwards."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Speaking Mode on Chat. Speak Sentence 1: "Tell me about the history of computers." | Transcription appears in input field |
| 2 | Pause ~2 seconds. Do not stop recording. Observe chat thread. | No message sent during the pause |
| 3 | Continue immediately with Sentence 2: "And include milestones from 1950 onwards." | Input field adds Sentence 2 to the existing transcription |
| 4 | Stop speaking completely. | Auto-send fires; both sentences appear as one message in chat |

## Expected Final State

Auto-send fires; both sentences appear as one message in chat

## Pass/Fail Criteria

**Pass:**
- No send during pause; both sentences sent as one message

**Fail:**
- Message sends after Sentence 1 pause; Sentence 2 sent separately or lost
