---
id: ELITEA-1298
title: "Speaking Mode — Auto-Send Fires After User Stops Speaking"
priority: critical
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1298: Speaking Mode — Auto-Send Fires After User Stops Speaking

**Module:** Speaking Mode · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that Speaking Mode automatically sends the message after silence — no Send button click required.

**Coverage:** Message auto-submits after speech ends; appears in chat thread without manual confirmation.

## Preconditions

- Speaking Mode active on Chat page; mic permission granted

## Test Data

Phrase: "Summarize what artificial intelligence is"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Speaking Mode on Chat. Speak: "Summarize what artificial intelligence is". | Transcription appears in input field |
| 2 | Stop speaking and stay silent. Do not click any button. | Message auto-sends; appears in chat thread; input clears |

## Expected Final State

Message auto-sends; appears in chat thread; input clears

## Pass/Fail Criteria

**Pass:**
- Message sent automatically without pressing Send

**Fail:**
- Message not sent — requires manual Send button click
