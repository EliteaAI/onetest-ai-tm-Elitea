---
id: ELITEA-1313
title: "Voice Settings Dialog — Speed and Volume Sliders Adjust Playback"
priority: critical
type: functional
module: voice-configuration-settings
status: ready
execution_type: automated
automation_test_id:
  - test_voice_configuration.py:TestVoiceConfiguration.test_speed_and_volume_controls
tags: [voice-settings, volume-slider, speed-slider, feat:voice, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5010]
---
# ELITEA-1313: Voice Settings Dialog — Speed and Volume Sliders Adjust Playback

**Module:** Voice Configuration Settings · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Speed and Volume sliders in the Voice Settings dialog control TTS playback rate and volume across their full ranges.

**Coverage:**
- Speed slider range: 0.5x (slowest) to 2x (fastest), default 1x
- Dragging Speed slider to min/max produces audibly different speech rates
- Volume slider range: Mute to 100%, default 100%
- Dragging Volume to Mute silences playback; 100% restores full volume
- Apply is required to activate slider changes
- Changes affect subsequent TTS playback immediately after Apply

## Preconditions

- User is logged in to {{base_url}}
- Active Chat conversation with at least one AI response
- TTS playback gear icon accessible
- System audio is active and audible

## Test Data

- URL: {{base_url}}
- Speed test values: 0.5x (leftmost), 1x (center), 2x (rightmost)
- Volume test values: Mute (leftmost), 50% (center), 100% (rightmost)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open Voice Settings dialog from TTS controls | Dialog opens; Speed slider is at 1x (center); Volume slider is at 100% (rightmost) |
| 2 | Drag the Speed slider to the leftmost position (0.5x) | Slider shows 0.5x label/position |
| 3 | Click Apply, then trigger TTS playback on an AI response | Speech is noticeably slower than normal speed |
| 4 | Reopen Voice Settings, drag Speed slider to the rightmost position (2x), click Apply | Slider shows 2x; TTS playback is noticeably faster than normal |
| 5 | Reopen Voice Settings, set Speed to center (1x), click Apply | Normal speech rate is restored |
| 6 | Reopen Voice Settings, drag Volume slider to leftmost position (Mute), click Apply | Slider is at Mute position |
| 7 | Trigger TTS playback | TTS plays silently — no audible output |
| 8 | Reopen Voice Settings, drag Volume to 50%, click Apply, trigger TTS | TTS plays at noticeably reduced volume |
| 9 | Reopen Voice Settings, drag Volume to 100%, click Apply, trigger TTS | TTS plays at full volume |

## Expected Final State

TTS plays at full volume

## Pass/Fail Criteria

**Pass:**
- Speed slider range is 0.5x–2x; audible difference at min/max vs default
- Volume Mute silences playback; 100% restores full volume
- All changes take effect after clicking Apply

**Fail:**
- Sliders have no audible effect on playback
- Slider range is incorrect or slider is non-interactive
- Volume Mute position still produces audible output
- Changes apply without clicking Apply (or do not apply after Apply)
