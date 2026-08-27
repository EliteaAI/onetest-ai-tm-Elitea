---
id: ELITEA-2816
title: "Chat – Follow-Up Suggestions Are Skipped for Very Short AI Replies (Eligibility Threshold Boundary)"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2816: Chat – Follow-Up Suggestions Are Skipped for Very Short AI Replies (Eligibility Threshold Boundary)

**Module:** chat-interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify AI replies shorter than the configured minimum length do not trigger suggestion generation, and that the boundary itself behaves correctly one unit below/above the threshold.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- Admin Portal minimum character/length threshold is at its default value.

---

## Test Data

| Field | Value |
|-------|-------|
| Prompt A | A prompt engineered to produce a reply just below the configured minimum length |
| Prompt B | A prompt engineered to produce a reply just at/above the configured minimum length |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Send Prompt A and wait for the AI response to complete | Reply length is confirmed just below threshold |
| 2 | Observe whether a suggestion request fires and whether chips render | No suggestion request/chip list |
| 3 | Send Prompt B and wait for the AI response to complete | Reply length is confirmed at/above threshold |
| 4 | Observe whether a suggestion request fires and whether chips render | Suggestion request fires and chip list renders normally |

---

## Expected Final State

Suggestion eligibility is gated strictly by the configured minimum-length threshold, with correct behavior on both sides of the boundary.

---

## Pass/Fail Criteria

**Pass:**
- Below-threshold reply produces no suggestion request/UI.
- At/above-threshold reply produces suggestions normally.

**Fail:**
- A below-threshold reply still produces suggestions.
- An at/above-threshold reply is incorrectly skipped.
