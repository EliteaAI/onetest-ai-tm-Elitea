---
id: ELITEA-1321
title: "Cancel, Stop and Restart Dictation Session"
priority: high
type: functional
module: voice-input
status: ready
execution_type: manual
tags: [nfr:accessibility, feature:4499, feat:voice, restart, r-2.0.3, session]
requirements: [EliteaAI/elitea_issues#4499]
---
# ELITEA-1321: Cancel, Stop and Restart Dictation Session

**Module:** Voice Input · **Priority:** High · **Type:** Functional

**Objective:** Verify that stopping dictation without sending does not submit a message, and that restarting a new dictation session appends new speech to existing transcription without duplication or overwrite.

**Coverage:**
- Stopping recording without pressing Send does not submit any message
- Restarting recording opens a clean session without clearing existing input
- New speech is appended to previously transcribed text on restart
- No text duplication from the previous session on restart
- No overwrite of previously transcribed text

## Preconditions

- User is logged into ELITEA
- ASR model configured in the project
- Chat page open with empty input field
- Microphone permission granted
- Browser: Chrome or Edge

## Test Data

- First spoken phrase: "First sentence"
- Second spoken phrase: "Second sentence"
- Expected combined input after two sessions: both phrases combined (e.g. "First sentence. Second sentence")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the microphone icon. Speak "First sentence". Pause. Click the microphone icon to stop recording. | "First sentence" (or similar transcription) appears in the input field. No message is submitted to the chat. |
| 2 | Check the chat conversation history. | No new message appears in the conversation — stopping without pressing Send does not submit anything. |
| 3 | Click the microphone icon again to start a new recording session. | Recording starts. Existing text in the input field is NOT cleared. |
| 4 | Speak "Second sentence". Pause. Click the microphone icon to stop recording. | Input field now contains both phrases combined. No duplication of "First sentence". The first phrase is not overwritten. |

## Expected Final State

Input field now contains both phrases combined. No duplication of "First sentence". The first phrase is not overwritten.

## Pass/Fail Criteria

**Pass:**
- No message submitted after stopping recording without Send
- Second recording session appends to first transcription without clearing it
- No duplication of text from the first session on restart
- Both phrases are combined correctly in the input field

**Fail:**
- Message is submitted automatically when recording stops
- Second session overwrites the content from the first session
- First phrase is duplicated when the second session starts
