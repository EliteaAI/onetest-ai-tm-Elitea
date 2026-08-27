---
id: ELITEA-2814
title: "Chat – Global Follow-Up Suggestions Flag OFF Suppresses Both the Request and the UI"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2814: Chat – Global Follow-Up Suggestions Flag OFF Suppresses Both the Request and the UI

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that with the global follow-up suggestions feature flag OFF, no suggestion network request is issued at all (not merely hidden in the UI), and no chip list renders.

---

## Preconditions

- Admin has set the global follow-up suggestions feature flag to OFF.
- User is logged in to the Elitea platform with an open conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | Any prompt that would otherwise be suggestion-eligible |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Confirm the global flag is OFF via Admin Portal | Flag shows OFF |
| 2 | Send the message and wait for the AI response to complete, while monitoring network traffic | No suggestion-related network request is made |
| 3 | Observe the composer area | No chip list renders above the composer |

---

## Expected Final State

With the global flag OFF, the feature is fully inert — no backend call and no UI element.

---

## Pass/Fail Criteria

**Pass:**
- No suggestion request is observed in network traffic.
- No chip list or suggestion UI renders.

**Fail:**
- A suggestion request is made despite the flag being OFF.
- Any suggestion UI element renders even without a visible chip list (e.g. an empty container).
