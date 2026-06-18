---
id: ELITEA-1290
title: "Speaking Mode — Manual Input Edit Resets Auto-Send Timer [Bug EliteaAI/elitea_issues#5029]"
priority: high
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5029, EliteaAI/elitea_issues#5016]
---
# ELITEA-1290: Speaking Mode — Manual Input Edit Resets Auto-Send Timer [Bug EliteaAI/elitea_issues#5029]

**Module:** Speaking Mode · **Priority:** High · **Type:** Functional

**Objective:** Verify that editing the transcribed text manually resets the auto-send timer — preventing premature send while user is still editing.

**Coverage:** Auto-send halted during typing; timer resets from last edit; edited text is what gets sent.

## Preconditions

- Speaking Mode active on Chat; mic granted

## Test Data

Spoken: "Schedule a meeting for tomorrow afternoon" → edit to add " at 2pm"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Enable Speaking Mode. Speak: "Schedule a meeting for tomorrow afternoon". Stop speaking → transcription appears and timer begins. | Transcription in input field; auto-send timer running |
| 2 | Before auto-send fires, click into the input field and type " at 2pm". | Text appended; no auto-send while typing |
| 3 | Stop typing. Wait for inactivity timeout. | Auto-send fires after timeout from last edit |
| 4 | Check the message sent in chat. | Message reads: "Schedule a meeting for tomorrow afternoon at 2pm" |

## Expected Final State

Message reads: "Schedule a meeting for tomorrow afternoon at 2pm"

## Pass/Fail Criteria

**Pass:**
- No send occurs while typing in the field; edited text is sent after inactivity timeout from last edit

**Fail:**
- Message sends while user is still editing; original unedited text is sent
