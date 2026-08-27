---
id: ELITEA-2825
title: "Chat – Regenerating a Response Correctly Resets Follow-Up Suggestions, Including In-Flight Requests"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6123, issue:6254]
requirements: [EliteaAI/elitea_issues#6123, EliteaAI/elitea_issues#6254]
---

# ELITEA-2825: Chat – Regenerating a Response Correctly Resets Follow-Up Suggestions, Including In-Flight Requests

**Module:** chat-interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify using the existing "Regenerate response" action clears the prior suggestion chip list, discards any suggestion request still in flight for the original response, and correctly resets composer/chip state if a chip's text had already been inserted.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- User has a conversation with a suggestion-eligible AI response and rendered chips.

---

## Test Data

| Field | Value |
|-------|-------|
| Message | Any prompt that produces a suggestion-eligible AI response |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | With chips rendered for the current response, click "Regenerate response" | Prior chip list clears immediately |
| 2 | Wait for the regenerated response to complete | A fresh suggestion list may render for the new response, independent of the discarded one |
| 3 | Repeat the flow, but click "Regenerate response" while the suggestion request for the *original* response is still in flight (e.g. slow backend) | The stale in-flight suggestion result, if it lands late, never renders after regeneration has produced its own response |
| 4 | Repeat again; click a chip to insert its (unedited) text into the input, then click "Regenerate response" | Both the input text and the chip list reset consistently — no leftover mismatched suggestion tied to the discarded response |

---

## Expected Final State

Regeneration always leaves the chip list and composer in a state consistent with the newly regenerated response, with no stale suggestion artifacts from the discarded response.

---

## Pass/Fail Criteria

**Pass:**
- Chip list clears on regenerate and refreshes consistently with the new response.
- A late-arriving stale suggestion request from the discarded response never renders.
- Composer/chip state resets consistently when a chip's text had been inserted before regeneration.

**Fail:**
- A stale suggestion list or late in-flight result renders after regeneration.
- Leftover chip text or a mismatched suggestion remains after regeneration.
