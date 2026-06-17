---
id: ELITEA-1283
title: "Speaking Mode — Rapid Toggling Leaves No Orphaned Sessions"
priority: medium
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1283: Speaking Mode — Rapid Toggling Leaves No Orphaned Sessions

**Module:** Speaking Mode · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that rapidly toggling between Speaking Mode and Voice Input leaves no orphaned microphone sessions, zombie WebSocket connections, or UI desync.

**Coverage:** Multiple rapid ON/OFF toggles across both modes; no zombie network sessions; chat remains functional after toggles.

## Preconditions

- Chat page; mic granted; browser DevTools Network tab open and recording

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Rapidly toggle: Speaking Mode ON → OFF → Voice Input ON → OFF → Speaking Mode ON. Repeat this cycle 3–5 times quickly. | UI responds to each toggle; no errors thrown |
| 2 | Check DevTools Network → WebSocket/SSE connections. | Only active mode's connection visible; no orphaned/zombie connections from previous sessions |
| 3 | Speak a sentence → observe transcription and auto-send. | Transcription appears correctly; message auto-sends; chat functional |

## Expected Final State

Transcription appears correctly; message auto-sends; chat functional

## Pass/Fail Criteria

**Pass:**
- No zombie socket events in DevTools; UI is consistent; voice transcription and auto-send work normally after toggles

**Fail:**
- Zombie WebSocket events detected; input field frozen; mic cannot re-activate; UI shows incorrect mode state
