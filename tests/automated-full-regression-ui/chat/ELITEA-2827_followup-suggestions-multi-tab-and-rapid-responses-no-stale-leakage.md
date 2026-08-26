---
id: ELITEA-2827
title: "Chat – Follow-Up Suggestions Do Not Leak Across Tabs or Show Stale Chips After Rapid Consecutive Responses"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2827: Chat – Follow-Up Suggestions Do Not Leak Across Tabs or Show Stale Chips After Rapid Consecutive Responses

**Module:** chat-interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that for the same user with the same conversation open in two browser tabs, suggestions generated in Tab A never appear in Tab B; and that sending two messages back-to-back before reading either response never leaves stale suggestions from the earlier response visible.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- Same user has the same conversation open in two browser tabs (Tab A, Tab B).

---

## Test Data

| Field | Value |
|-------|-------|
| Message 1, Message 2 | Two distinct suggestion-eligible prompts, sent back-to-back |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | In Tab A, send a suggestion-eligible message and wait for chips to render | Chips render in Tab A |
| 2 | Switch to Tab B (same conversation, same user) without reloading | Chips from Tab A's turn are not visible in Tab B |
| 3 | In a single tab, send Message 1, then immediately send Message 2 before Message 1's response/chips have had time to fully resolve | Only the chip list belonging to the most recent completed response (Message 2's) is ever shown; no stale chips from Message 1's response appear |

---

## Expected Final State

Suggestion state is strictly per-tab and always reflects only the latest completed response in that tab.

---

## Pass/Fail Criteria

**Pass:**
- Tab B never shows chips generated in Tab A.
- Rapid consecutive responses never leave a stale earlier chip list visible.

**Fail:**
- Chips from one tab appear in another tab for the same conversation/user.
- A stale chip list from an earlier response remains visible after a later response completes.
