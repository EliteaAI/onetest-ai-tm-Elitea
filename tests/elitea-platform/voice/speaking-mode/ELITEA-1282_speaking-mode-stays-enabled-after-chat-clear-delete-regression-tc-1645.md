---
id: ELITEA-1282
title: "Speaking Mode — Stays Enabled After Chat Clear/Delete [Regression TC-1645]"
priority: medium
type: functional
module: speaking-mode
status: ready
execution_type: manual
tags: [feature:5016, feat:voice, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5016]
---
# ELITEA-1282: Speaking Mode — Stays Enabled After Chat Clear/Delete [Regression TC-1645]

**Module:** Speaking Mode · **Priority:** Medium · **Type:** Functional

**Objective:** Verify Speaking Mode remains ON after clearing the chat history or deleting individual messages — mode should not be affected by chat content operations. Regression check for TC-1645.

**Coverage:** Clear Chat → mode stays ON; Delete response → mode stays ON; voice still works after both operations.

## Preconditions

- Speaking Mode active; at least one exchange (user message + AI response) exists in chat

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | With Speaking Mode ON, click Clear Chat (or equivalent button to clear history). | Chat history clears; Speaking Mode indicator still shows ON |
| 2 | Speak a sentence → transcription appears and auto-sends. Receive AI response. | Voice input and auto-send work normally after clear |
| 3 | Click Delete on the AI response to remove it. | Response removed; Speaking Mode indicator still shows ON |
| 4 | Speak another sentence → confirm auto-send still works. | Message transcribed and sent; Speaking Mode fully functional |

## Expected Final State

Message transcribed and sent; Speaking Mode fully functional

## Pass/Fail Criteria

**Pass:**
- Speaking Mode indicator stays ON after Clear Chat and after deleting a response; voice transcription and auto-send work after both operations

**Fail:**
- Speaking Mode turns off after Clear Chat or Delete; user must re-enable
