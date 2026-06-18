---
id: ELITEA-1285
title: "Speaking Mode — Browser Tab Switch Does Not Disable Speaking Mode"
priority: high
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1285: Speaking Mode — Browser Tab Switch Does Not Disable Speaking Mode

**Module:** Speaking Mode · **Priority:** High · **Type:** Functional

**Objective:** Verify that switching to another browser tab and returning does not disable Speaking Mode — mode remains ON and voice input continues to work.

**Coverage:** Switch away → return → indicator still ON; voice transcription and auto-send functional.

## Preconditions

- Speaking Mode active on Chat page; second browser tab available

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm Speaking Mode indicator is ON on the ELITEA Chat tab. | Speaking Mode active |
| 2 | Click on another browser tab. Wait 5–10 seconds. | ELITEA tab is in background |
| 3 | Switch back to the ELITEA tab. Check the Speaking Mode indicator. | Indicator still shows ON |
| 4 | Speak a sentence → observe transcription and auto-send. | Transcription appears; message auto-sends correctly |

## Expected Final State

Transcription appears; message auto-sends correctly

## Pass/Fail Criteria

**Pass:**
- Speaking Mode indicator still ON after returning to ELITEA tab; voice transcription and auto-send work normally

**Fail:**
- Speaking Mode disabled when user switches back; must re-enable manually
