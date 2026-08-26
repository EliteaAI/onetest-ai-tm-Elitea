---
id: ELITEA-2811
title: "Chat – Follow-Up Suggestion Generation Fires Only After Full AI Response, Never Delays Main Response"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2811: Chat – Follow-Up Suggestion Generation Fires Only After Full AI Response, Never Delays Main Response

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify the follow-up suggestion request is only issued after the AI response has fully finished streaming, and that enabling the feature does not delay or alter delivery of the main AI response.

---

## Preconditions

- User is logged in to the Elitea platform.
- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- User has an open conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| Message A | Any prompt producing a normal-length AI response, sent with the feature flag ON |
| Message B | The same prompt, sent in an otherwise identical conversation with the feature flag OFF |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Send Message A while monitoring network traffic and the response stream | No suggestion request is made while the AI response is still streaming |
| 2 | Wait for the AI response to finish streaming completely | A suggestion request fires only after the response is fully delivered |
| 3 | Record the time from send to full response completion | Time is recorded as baseline-with-feature-ON |
| 4 | Send Message B (feature flag OFF) and record the same completion time | Time recorded as baseline-with-feature-OFF |
| 5 | Compare the two completion times | No perceptible delay/difference attributable to suggestion generation |

---

## Expected Final State

The main AI response streams and completes identically whether or not the follow-up suggestion feature is enabled; the suggestion request is observably issued only after response completion.

---

## Pass/Fail Criteria

**Pass:**
- Suggestion request network call is only observed after the AI response stream has fully ended.
- Response completion timing is not measurably slower with the feature ON vs OFF.

**Fail:**
- A suggestion request is observed before or during response streaming.
- The main response is delayed, blocked, or altered by suggestion generation.
