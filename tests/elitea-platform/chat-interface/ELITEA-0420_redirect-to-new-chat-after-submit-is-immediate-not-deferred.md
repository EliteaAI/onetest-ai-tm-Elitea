---
id: ELITEA-0420
title: "Redirect to New Chat After Submit Is Immediate, Not Deferred"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:chat, ui]
requirements: [ProjectAlita/projectalita.github.io#3933]
---
# ELITEA-0420: Redirect to New Chat After Submit Is Immediate, Not Deferred

**Module:** Chat Interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that after clicking Submit on the warning modal during an active generation, the redirect to the new chat happens immediately — without waiting for the previous run to finish.

**Coverage:**
- User is no longer on the previous conversation immediately after Submit
- New chat view loads while the previous run would still be in progress
- New chat view is clean and ready for input

## Preconditions

- Logged in to {{base_url}} with Chat access
- Existing conversation with an LLM model or agent participant
- Chrome (latest)

## Test Data

- Prompt: "Write a detailed 10-paragraph essay about climate change."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Open a conversation with an LLM model or agent. | Conversation is open. |
| 2 | Send: "Write a detailed 10-paragraph essay about climate change." Note the time. | Response begins streaming. |
| 3 | Within 2–3 seconds of response start (while clearly still streaming), click + Create in the Chat sidebar. | Warning modal appears: "Output is still generating. Switching now will stop it and you may lose progress. Switch anyway?" |
| 4 | Click Submit. | Modal closes. |
| 5 | Observe the screen state immediately (within 1–2 seconds of clicking Submit). | User is no longer on the previous conversation. The previous streaming response is not visible. |
| 6 | Confirm the new chat view is displayed. | Empty chat input field and welcome state are shown. No previous conversation content is visible. |
| 7 | Confirm the switch did not require the previous run to complete. | The new chat view appeared before the previous run's expected completion time. |

## Expected Final State

The new chat view appeared before the previous run's expected completion time.

## Pass/Fail Criteria

**Pass:**
- User is redirected to a new chat view within 1–2 seconds of clicking Submit
- Previous conversation is no longer displayed immediately after Submit
- New chat shows empty, clean state ready for input

**Fail:**
- User remains on the previous conversation after clicking Submit
- Redirect only occurs after the previous run finishes streaming
- New chat view fails to load or retains previous conversation content
