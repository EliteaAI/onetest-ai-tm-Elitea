---
id: ELITEA-2815
title: "Chat – Per-Project Disallow-List Suppresses Follow-Up Suggestions for That Project Only"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2815: Chat – Per-Project Disallow-List Suppresses Follow-Up Suggestions for That Project Only

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify that with the global flag ON, a project on the Admin Portal disallow-list gets no suggestions, while a project not on the list behaves normally.

---

## Preconditions

- Admin has set the global follow-up suggestions feature flag to ON.
- Project P1 is added to the Admin Portal Disallowed Projects list; Project P2 is not on the list.
- User has access to both P1 and P2, each with an open conversation.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | Any prompt that would otherwise be suggestion-eligible, sent identically in both projects |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | In Project P1 (disallowed), send the message and wait for the AI response | No suggestion request is made and no chip list renders |
| 2 | Switch to Project P2 (not disallowed) and send the same message | Suggestion request is made and chip list renders normally |
| 3 | Switch back to Project P1 and repeat with a different message | Still no suggestions for P1 |

---

## Expected Final State

Suggestion behavior is gated per-project by the disallow-list, independent of the global flag being ON.

---

## Pass/Fail Criteria

**Pass:**
- Disallowed project P1 never produces a suggestion request or chip list.
- Non-disallowed project P2 produces suggestions normally.

**Fail:**
- Suggestions appear for a disallowed project.
- Suggestions are missing for a non-disallowed project when the global flag is ON.
