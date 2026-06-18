---
id: ELITEA-1326
title: "Microphone Icon Visual States and Tooltip"
priority: critical
type: functional
module: voice-input
status: ready
execution_type: manual
tags: [nfr:accessibility, feature:4499, feat:voice, r-2.0.3, visual, ui]
requirements: [EliteaAI/elitea_issues#4499]
---
# ELITEA-1326: Microphone Icon Visual States and Tooltip

**Module:** Voice Input · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the microphone icon correctly reflects its idle and active recording states through visual styling, and that a descriptive tooltip is shown on hover.

**Coverage:**
- Tooltip text displayed on hover in idle state and during active recording
- Icon visual change (color, style) when recording starts
- Input field border and glow styling during active recording
- Icon and input field border revert to default after recording stops

## Preconditions

- User is logged into ELITEA
- ASR model configured in the project
- Chat page open
- Browser: Chrome or Edge

## Test Data

- Expected idle tooltip: "Start voice input"
- Expected active tooltip: "Voice input active"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Hover the mouse over the microphone icon in the idle state without clicking. | A tooltip appears with text "Start voice input". |
| 2 | Click the microphone icon to start recording. | The icon changes to its active appearance (different color — teal/primary). The input field container displays a primary-color glowing border/shadow. |
| 3 | Hover over the active microphone icon while recording. | Tooltip text displays "Voice input active". |
| 4 | Click the microphone icon to stop recording. | The icon reverts to its default inactive appearance. The input field border/glow returns to its default state. |

## Expected Final State

The icon reverts to its default inactive appearance. The input field border/glow returns to its default state.

## Pass/Fail Criteria

**Pass:**
- Tooltip text is present and accurate in both idle and recording states
- Icon appearance visually distinguishes idle vs. recording state
- Input field border shows recording glow during active recording and reverts after stopping

**Fail:**
- No tooltip appears on hover in either state
- Icon appearance does not change between idle and recording states
- Input border/glow does not reflect recording state
