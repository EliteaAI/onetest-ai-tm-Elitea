---
id: ELITEA-1312
title: "Voice Settings Dialog Opens and Displays All Controls Including Voice Selector"
priority: critical
type: functional
module: voice-configuration-settings
status: ready
execution_type: automated
automation_test_id:
  - test_voice_configuration.py:TestVoiceConfiguration.test_voice_selection_from_chat
tags: [voice-selection, voice-settings, feat:voice, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5010]
---
# ELITEA-1312: Voice Settings Dialog Opens and Displays All Controls Including Voice Selector

**Module:** Voice Configuration Settings · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Voice Settings dialog opens from the Chat TTS playback controls and that all expected controls are present, including a functional Voice selector dropdown.

**Coverage:**
- Voice Settings dialog is accessible from the TTS "Read out" gear/settings icon
- Dialog contains: Voice dropdown, Speed slider (0.5x–2x), Volume slider (Mute–100%), Cancel button, Apply button
- Voice dropdown is populated with at least one voice option
- Selecting a different voice updates the dropdown display
- Apply saves the selection; Cancel closes without changes

## Preconditions

- User is logged in to {{base_url}}
- An active Chat conversation exists with at least one AI response
- TTS (Read out) is available on AI responses
- System audio is functional

## Test Data

- URL: {{base_url}}
- Default voice: Shimmer
- Alternative voice: any available option different from Shimmer

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat, send a message, and wait for AI response | AI response is displayed in the conversation |
| 2 | Click the 'Read out' (speaker) icon on the AI response | TTS playback begins; a playback control bar appears showing a gear/settings icon |
| 3 | Click the gear/settings icon in the TTS control bar | Voice Settings dialog opens |
| 4 | Inspect all dialog elements | Dialog contains: Voice selector dropdown (showing current voice e.g. 'Shimmer'), Speed slider (range 0.5x–2x), Volume slider (range Mute–100%), Cancel button, and Apply button |
| 5 | Click the Voice dropdown | Dropdown expands showing a non-empty list of available voice options |
| 6 | Select a voice different from the current one | Dropdown closes; the newly selected voice name is displayed |
| 7 | Click Apply | Dialog closes; selected voice is saved |
| 8 | Re-open Voice Settings dialog | Dialog shows the voice selected in step 6 — not the original default |
| 9 | Open Voice Settings again, change Voice, then click Cancel | Dialog closes; voice reverts to the previously applied selection |

## Expected Final State

Dialog closes; voice reverts to the previously applied selection

## Pass/Fail Criteria

**Pass:**
- Dialog opens from TTS gear icon
- All required controls are present (Voice, Speed, Volume, Cancel, Apply)
- Voice dropdown is populated with at least one option
- Apply persists the selected voice; Cancel discards the change

**Fail:**
- Dialog does not open
- Any control is missing or non-functional
- Voice dropdown is empty
- Apply does not save; Cancel saves when it should not
