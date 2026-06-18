---
id: ELITEA-1314
title: "Voice Settings Sync Between Chat Dialog and Personalization Page"
priority: medium
type: functional
module: voice-configuration-settings
status: ready
execution_type: automated
tags: [personalization, voice-settings, settings-sync, feat:voice, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5010]
---
# ELITEA-1314: Voice Settings Sync Between Chat Dialog and Personalization Page

**Module:** Voice Configuration Settings · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that voice configuration changes made via the Chat TTS dialog are reflected in User > Personalization and vice versa — both surfaces share the same persisted settings.

**Coverage:**
- Setting changed in Chat Voice Settings dialog is visible in Personalization Voice Personalization section
- Setting changed in Personalization Voice Personalization is visible in Chat Voice Settings dialog
- Both surfaces read from and write to the same user-level voice preferences
- TTS playback uses the most recently saved settings regardless of which surface was used to change them

## Preconditions

- User is logged in to {{base_url}}
- Active Chat conversation with at least one AI response
- TTS gear icon accessible
- Known baseline settings recorded (Voice, Speed, Volume)

## Test Data

- Chat URL: {{base_url}}
- Personalization URL: {{base_url}} (Personalization section)
- Baseline voice: Shimmer, Speed: 1x
- Modified Voice via Personalization: any voice different from Shimmer

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to User > Personalization; note current Voice and Speed values in the Voice Personalization section | Current values recorded (e.g., Shimmer, 1x) |
| 2 | In Personalization, change Voice to a different option (not Shimmer) | Voice dropdown updated |
| 3 | Navigate to Chat, trigger TTS, open Voice Settings dialog | Voice dropdown shows the voice selected in Personalization — not the previous value |
| 4 | Trigger TTS playback in Chat | Playback uses the voice changed in Personalization, confirming both surfaces share the same settings |

## Expected Final State

Playback uses the voice changed in Personalization, confirming both surfaces share the same settings

## Pass/Fail Criteria

**Pass:**
- Speed changed via Chat dialog is reflected in Personalization section
- Voice changed via Personalization is reflected in Chat dialog
- TTS playback uses the most recently saved value from either surface

**Fail:**
- Settings are siloed — changes in Chat do not appear in Personalization or vice versa
- One surface always overrides the other regardless of change order
- TTS playback uses stale settings after cross-surface update
