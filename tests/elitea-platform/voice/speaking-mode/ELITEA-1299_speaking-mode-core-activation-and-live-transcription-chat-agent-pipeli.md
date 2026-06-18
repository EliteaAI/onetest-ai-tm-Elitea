---
id: ELITEA-1299
title: "Speaking Mode Core Activation and Live Transcription [Chat, Agent, Pipeline]"
priority: critical
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1299: Speaking Mode Core Activation and Live Transcription [Chat, Agent, Pipeline]

**Module:** Speaking Mode · **Priority:** Critical · **Type:** Functional

**Objective:** Verify clicking the Speaking Mode button activates mic capture and live speech is transcribed into the input field — on Chat, Agent, and Pipeline pages.

**Coverage:** Mic activation, live transcription in input field, consistent across all 3 pages.

## Preconditions

- Mic permission granted; mic hardware functional; input field empty on each page

## Test Data

Phrase: "What is today's date?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Ensure input is empty. Click the Speaking Mode button. | Mic activates; OS/browser mic indicator shows active |
| 2 | Speak: "What is today’s date?" | Text appears live in the input field |
| 3 | Repeat steps 1–2 on the Agent execution panel. | Transcription works on Agent page |
| 4 | Repeat steps 1–2 on the Pipeline execution panel. | Transcription works on Pipeline page |

## Expected Final State

Transcription works on Pipeline page

## Pass/Fail Criteria

**Pass:**
- Mic activates and transcription appears live on all 3 pages

**Fail:**
- No activation or no transcription on any page
