---
id: ELITEA-1293
title: "Speaking Mode Available on Agent Page with No Prior Messages [Bug #4994]"
priority: high
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4994, EliteaAI/elitea_issues#5016]
---
# ELITEA-1293: Speaking Mode Available on Agent Page with No Prior Messages [Bug #4994]

**Module:** Speaking Mode · **Priority:** High · **Type:** Functional

**Objective:** Verify Speaking Mode is available and activatable on the Agent page in an empty execution session.

**Coverage:** Button present on Agent page with no prior messages; activation and transcription work.

## Preconditions

- Agent page open; mic permission granted; execution session has no prior messages

## Test Data

Phrase: "What can you help me with?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an Agent's Test Settings / execution panel. Clear session if any messages exist. | Empty session with no messages |
| 2 | Observe the input toolbar. | Speaking Mode button is visible and clickable |
| 3 | Click the Speaking Mode button. Speak: "What can you help me with?" | Mode activates; transcription appears; message auto-sends |

## Expected Final State

Mode activates; transcription appears; message auto-sends

## Pass/Fail Criteria

**Pass:**
- Speaking Mode available and works on Agent page with empty session

**Fail:**
- Button absent or error when activating before first message
