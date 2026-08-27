---
id: ELITEA-2818
title: "Chat – Follow-Up Suggestion Failure, Timeout, or Empty Result Is a Silent No-Op"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2818: Chat – Follow-Up Suggestion Failure, Timeout, or Empty Result Is a Silent No-Op

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that when suggestion generation fails, times out, or returns an empty result, the user sees no error message, no retry control, no loading spinner, and no empty-state text — the chip area simply stays absent.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- Ability to simulate a suggestion-generation failure, timeout, or empty response (e.g. via a deliberately slow/broken backend model, or a test hook).

---

## Test Data

| Field | Value |
|-------|-------|
| Scenario A | Suggestion backend returns an error |
| Scenario B | Suggestion backend exceeds the configured generation timeout |
| Scenario C | Suggestion backend returns an empty/blank result |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Trigger Scenario A and send a suggestion-eligible message | No error message, toast, retry button, spinner, or empty-state text appears in the composer area |
| 2 | Trigger Scenario B and send a suggestion-eligible message | Once the timeout elapses, the same silent no-op behavior is observed |
| 3 | Trigger Scenario C and send a suggestion-eligible message | The same silent no-op behavior is observed |
| 4 | In each scenario, confirm the main AI response rendered normally and unaffected | Main chat response is complete and correct in all three scenarios |

---

## Expected Final State

None of the three failure modes produce any visible UI artifact beyond the simple absence of chips; the main chat experience is unaffected.

---

## Pass/Fail Criteria

**Pass:**
- All three scenarios result in no chip list and no visible error/loading/empty-state UI.
- Main AI response is unaffected in all three scenarios.

**Fail:**
- Any scenario shows an error message, spinner, retry control, or empty-state text.
- The main AI response is delayed, broken, or altered by any of the failure scenarios.
