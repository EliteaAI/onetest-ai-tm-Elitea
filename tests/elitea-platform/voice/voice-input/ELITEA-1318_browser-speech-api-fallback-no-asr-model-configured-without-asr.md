---
id: ELITEA-1318
title: "Browser Speech API Fallback — No ASR Model Configured [Without ASR]"
priority: critical
type: functional
module: voice-input
status: ready
execution_type: manual
tags: [nfr:accessibility, known-issues, feature:4499, browser-api, feat:voice, fallback, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4499]
---
# ELITEA-1318: Browser Speech API Fallback — No ASR Model Configured [Without ASR]

**Module:** Voice Input · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the browser Speech API fallback behavior when no ASR model is configured — Chrome/Edge show the mic button via the browser API while Firefox hides it entirely. Known bugs with the fallback path are documented.

**Coverage:**
- Chrome: mic button visible without ASR model (browser Web Speech API active)
- Firefox: mic button NOT visible without ASR model (browser API unsupported — expected behavior)
- Browser fallback transcription is word-by-word (real-time), unlike server ASR (sentence-by-sentence)
- Known bug: manual edits during active recording are overridden by new speech — not planned to fix (issue #4885)
- Known limitation: spoken punctuation words not converted to symbols in fallback mode

## Preconditions

- User is logged into ELITEA
- NO ASR model is configured in the project (verify via empty socket during the Voice-to-Text)?include_shared=true&section=asr returns empty items array)
- Microphone permission granted in Chrome
- Test performed in both Chrome and Firefox

## Test Data

- Browsers: Chrome (fallback active), Firefox (no button expected)
- First spoken phrase: "Hello world"
- Manual edit text: change "Hello world" to "Hello edited"
- Second spoken phrase (while still recording): "New words"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Chat page in Chrome with no ASR model configured. Check the input toolbar. | Microphone icon IS visible (Chrome supports Web Speech API as fallback even without a server ASR model). |
| 2 | Click the microphone icon, speak "Hello world", and observe transcription appearing. | Words appear progressively in the input field in real-time as spoken (word-by-word), which differs from server ASR that appends sentence-by-sentence after a pause. |
| 3 | While recording is still active, manually edit the transcribed text (change "Hello world" to "Hello edited"). Then speak "New words" while recording remains active. | [KNOWN BUG — not planned to fix, issue #4885] The manual edit is overridden — the input field is restored to the previous transcribed state when new speech is detected. Manual edits cannot be preserved during an active browser fallback recording session. |
| 4 | Stop the recording. Open the Chat page in Firefox with no ASR model configured. Check the input toolbar. | Microphone icon is NOT visible in Firefox. This is expected — Firefox does not support the browser Web Speech API and no server ASR is configured. |

## Expected Final State

Microphone icon is NOT visible in Firefox. This is expected — Firefox does not support the browser Web Speech API and no server ASR is configured.

## Pass/Fail Criteria

**Pass:**
- Microphone button visible in Chrome when no ASR model is configured ✓
- Real-time word-by-word transcription works in Chrome fallback ✓
- Microphone button NOT visible in Firefox when no ASR model configured ✓ (expected behavior)

**Fail:**
- Microphone button missing in Chrome when no ASR model is configured
- Transcription does not work in Chrome fallback
- Microphone button visible in Firefox with no ASR model (unexpected)

**Known Bugs (won't-fix — not treated as test failure):**
- Manual edits during active recording are overridden when new speech arrives — see issue #4885 (closed as not planned)
- Spoken punctuation words ("comma", "period", "question mark") are not converted to symbols in browser fallback mode
