---
id: ELITEA-1315
title: "Apply Saves and Cancel Discards Voice Settings Changes"
priority: high
type: functional
module: voice-configuration-settings
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.voice.test_voice_configuration.TestVoiceConfiguration.test_voice_selection_from_chat
tags: [voice-settings, feat:voice, r-2.0.4, cancel, apply]
requirements: [EliteaAI/elitea_issues#5010]
---
# ELITEA-1315: Apply Saves and Cancel Discards Voice Settings Changes

**Module:** Voice Configuration Settings · **Priority:** High · **Type:** Functional

**Objective:** Verify that Apply persists voice configuration changes and affects playback, while Cancel discards all pending changes and leaves previous settings intact.

**Coverage:**
- Apply closes dialog and saves all changed settings (voice, speed, volume)
- TTS playback after Apply uses the newly saved settings
- Reopening dialog after Apply shows the saved values
- Cancel closes dialog without saving any pending changes
- TTS playback after Cancel continues using the pre-Cancel settings
- Reopening dialog after Cancel shows the original values

## Preconditions

- User is logged in to {{base_url}}
- Active Chat conversation with at least one AI response
- TTS gear icon accessible
- Known baseline settings: Voice = Shimmer, Speed = 1x, Volume = 100%

## Test Data

- URL: {{base_url}}
- Baseline voice: Shimmer, Speed: 1x, Volume: 100%
- Changed voice: any different available voice, Speed: 0.75x

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Voice Settings dialog; note current values (Voice, Speed, Volume) | Dialog shows known baseline values |
| 2 | Change Voice to a different option and move Speed slider to 0.75x | Dialog reflects the pending changes |
| 3 | Click Apply | Dialog closes without error |
| 4 | Trigger TTS playback on an AI response | Playback uses the newly selected voice and 0.75x speed (audibly different from baseline) |
| 5 | Reopen Voice Settings dialog | Dialog shows the updated voice and 0.75x speed — not the original baseline |
| 6 | Change Voice and Speed to yet another set of values | Dialog reflects the new pending changes |
| 7 | Click Cancel | Dialog closes |
| 8 | Trigger TTS playback | Playback still uses the settings from step 3 (Apply), not the values changed before Cancel |
| 9 | Reopen Voice Settings dialog | Dialog shows the step-3 applied values — changes made before Cancel are not present |

## Expected Final State

Dialog shows the step-3 applied values — changes made before Cancel are not present

## Pass/Fail Criteria

**Pass:**
- Apply saves all changed settings; playback and reopened dialog confirm the saved values
- Cancel discards all pending changes; playback and reopened dialog show pre-Cancel values

**Fail:**
- Apply closes dialog but settings revert to default on next open
- Cancel accidentally saves the pending changes
- Playback does not reflect the applied settings
