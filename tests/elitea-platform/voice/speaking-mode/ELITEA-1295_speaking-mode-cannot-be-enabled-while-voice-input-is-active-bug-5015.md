---
id: ELITEA-1295
title: "Speaking Mode Cannot Be Enabled While Voice Input Is Active [Bug #5015]"
priority: critical
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5015, EliteaAI/elitea_issues#5016]
---
# ELITEA-1295: Speaking Mode Cannot Be Enabled While Voice Input Is Active [Bug #5015]

**Module:** Speaking Mode · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Speaking Mode cannot be enabled while "Start Voice Input" is already active — the Speaking Mode button must be blocked/disabled when Voice Input session is running.

**Coverage:** Voice Input active → Speaking Mode button disabled or blocked; attempting to enable Speaking Mode has no effect; Voice Input session continues uninterrupted.

## Preconditions

- Chat page; mic permission granted; Voice Input is currently active (mic recording)

## Test Data

N/A

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Start Voice Input. Confirm it is active: mic indicator ON, Voice Input button shows active state. | Voice Input session running; mic capturing |
| 2 | Observe the Speaking Mode button while Voice Input is active. | Speaking Mode button is disabled, greyed out, or otherwise blocked — cannot be clicked |
| 3 | Attempt to click the Speaking Mode button. | Nothing happens — Speaking Mode does NOT activate; Voice Input continues uninterrupted |
| 4 | Verify the UI state: only Voice Input remains active. | Voice Input still ON; Speaking Mode still OFF; no dual-mode state |
| 5 | Stop Voice Input. Now attempt to enable Speaking Mode. | Speaking Mode activates successfully once Voice Input is no longer running |

## Expected Final State

Speaking Mode activates successfully once Voice Input is no longer running

## Pass/Fail Criteria

**Pass:**
- Speaking Mode button is blocked/disabled while Voice Input is active
- Clicking it has no effect; Voice Input continues
- Speaking Mode enables normally once Voice Input is stopped

**Fail:**
- Speaking Mode activates while Voice Input is still running
- Both modes active simultaneously
- Voice Input interrupted unexpectedly by the attempt
