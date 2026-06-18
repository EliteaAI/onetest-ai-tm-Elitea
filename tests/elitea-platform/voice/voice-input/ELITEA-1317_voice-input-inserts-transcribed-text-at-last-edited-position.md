---
id: ELITEA-1317
title: "Voice Input Inserts Transcribed Text at Last Edited Position"
priority: high
type: functional
module: voice-input
status: ready
execution_type: manual
tags: [text-editing, feature:4499, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4499]
---
# ELITEA-1317: Voice Input Inserts Transcribed Text at Last Edited Position

**Module:** Voice Input · **Priority:** High · **Type:** Functional

**Objective:** Verify that voice dictation inserts transcribed text at the last edited position in the input field, preserving all existing text.

**Coverage:**
- Last edited position is captured at the moment recording starts
- Spoken text is inserted at the last edited position
- Surrounding text is preserved unchanged
- Final result is correct and complete

## Preconditions

- User is logged into ELITEA
- ASR model configured in the project
- Chat page open with empty input field
- Microphone permission granted
- Browser: Chrome or Edge

## Test Data

- Pre-existing text: "Hello world"
- Visual cursor moved to: between "Hello" and "world" (mid-text)
- Last edited position: end of field (after "world") — this is where voice inserts
- Spoken phrase: "beautiful"
- Expected result: "Hello world beautiful" (inserted at last edited position, not at visual cursor)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Type "Hello world" into the chat input field. The last edited position is at the end of the field (after "world"). | Text "Hello world" appears in the input field; cursor at end |
| 2 | Click in the input field between "Hello" and "world" to visually move the cursor to the middle of the text (after the space, before "w"). | Cursor visually positioned mid-text between the two words |
| 3 | Click the microphone icon to start recording. | Recording starts |
| 4 | Speak the word "beautiful". Pause ~1 second for transcription flush. | "beautiful" is inserted at the last edited position (end of field, after "world") — NOT at the visual cursor position between the two words |
| 5 | Click the microphone icon to stop recording. Inspect the full input field text. | Final text reads "Hello world beautiful" — existing text preserved; "beautiful" appended at the last edited position |

## Expected Final State

Final text reads "Hello world beautiful" — existing text preserved; "beautiful" appended at the last edited position

## Pass/Fail Criteria

**Pass:**
- "beautiful" inserted at the last edited position (after "world"), result: "Hello world beautiful"
- Existing text ("Hello world") fully preserved

**Fail:**
- "beautiful" inserted at the visual cursor position (between "Hello" and "world"), result: "Hello beautiful world"
- Existing text overwritten or lost
