---
id: ELITEA-1294
title: "Speaking Mode Available in New Empty Chat Before First Message — Chat Page [Bug EliteaAI/elitea_issues#4994]"
priority: critical
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4994, EliteaAI/elitea_issues#5016]
---
# ELITEA-1294: Speaking Mode Available in New Empty Chat Before First Message — Chat Page [Bug EliteaAI/elitea_issues#4994]

**Module:** Speaking Mode · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the Speaking Mode button is present and functional in a brand new empty chat on the Chat page — before any messages have been sent.

**Coverage:** Button visible in new empty chat; mode activates without error; first message can be sent via Speaking Mode.

## Preconditions

- Chat page; mic permission granted

## Test Data

Phrase: "Hello, this is my first message using Speaking Mode"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a new conversation on Chat page. Confirm zero messages in the thread. | Empty conversation open |
| 2 | Ensure the input field is empty. Observe the input toolbar. | Speaking Mode button is visible and clickable (not greyed out or absent) |
| 3 | Click the Speaking Mode button. | Mode activates without error |
| 4 | Speak: "Hello, this is my first message using Speaking Mode". Stop speaking. | Transcription appears; message auto-sends; appears as first message in chat |

## Expected Final State

Transcription appears; message auto-sends; appears as first message in chat

## Pass/Fail Criteria

**Pass:**
- Speaking Mode available and fully functional in empty new chat

**Fail:**
- Button absent/greyed out; error on activation; requires first manual message before becoming available
