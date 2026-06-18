---
id: ELITEA-1322
title: "Append Voice to Existing Text and Cursor Position Insertion"
priority: high
type: functional
module: voice-input
status: deprecated
execution_type: manual
tags: [nfr:accessibility, text-editing, feature:4499, feat:voice, r-2.0.3, cursor]
requirements: [EliteaAI/elitea_issues#4499]
---
# ELITEA-1322: Append Voice to Existing Text and Cursor Position Insertion

**Module:** Voice Input · **Priority:** High · **Type:** Functional

**Objective:** **[DEPRECATED]** This test case assumed voice input inserts at the explicit cursor position. Actual behaviour inserts at the last edited position in the field. Replaced by the new TC "Voice Input Inserts Transcribed Text at Last Edited Position".

**Original Objective:** Verify that voice dictation inserts transcribed text at the current cursor position in the input field, preserving all existing text before and after the cursor.

## Preconditions

- User is logged into ELITEA
- ASR model configured in the project
- Chat page open with empty input field
- Microphone permission granted
- Browser: Chrome or Edge

## Test Data

- Pre-existing text: "Hello world"
- Cursor position: between "Hello " and "world" (after the space, before "w")
- Spoken phrase: "beautiful"
- Expected result after stop: "Hello beautiful world"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type "Hello world" into the chat input field. | Text "Hello world" appears in the input field |
| 2 | Click in the input field between "Hello " and "world" to place the cursor there (after the space, before the "w"). | Cursor is positioned between "Hello " and "world" |
| 3 | Click the microphone icon to start recording. | Recording starts with the cursor position captured |
| 4 | Speak the word "beautiful". Pause for ~1 second to allow transcription flush. | Input field shows a live preview with "beautiful" inserted at the cursor position, e.g. "Hello beautiful world" |
| 5 | Click the microphone icon to stop recording. | Final text in the input field reads "Hello beautiful world". Cursor is positioned immediately after "beautiful" |

## Expected Final State

Final text in the input field reads "Hello beautiful world". Cursor is positioned immediately after "beautiful"

## Pass/Fail Criteria

**Pass:**
- Spoken word "beautiful" is inserted at the cursor position between "Hello " and "world"
- Pre-cursor text ("Hello ") is unchanged
- Post-cursor text ("world") is unchanged
- Cursor is positioned after the inserted voice text after stopping

**Fail:**
- Existing text is overwritten or erased by the voice input
- Post-cursor text ("world") is lost after recording
