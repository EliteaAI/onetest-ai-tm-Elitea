---
id: ELITEA-2824
title: "Chat – Follow-Up Suggestion Chip List Does Not Overlap Composer, Attachments, Model Selector, or Send Button"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6254]
requirements: [EliteaAI/elitea_issues#6254]
---

# ELITEA-2824: Chat – Follow-Up Suggestion Chip List Does Not Overlap Composer, Attachments, Model Selector, or Send Button

**Module:** chat-interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the chip list, when rendered above the composer, never visually overlaps or obscures the message input, attached-files area, model selector, or send button, across common and narrow/mobile-ish viewport widths.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- A suggestion-eligible AI response has rendered a full 3-chip list, including at least one long suggestion.

---

## Test Data

| Field | Value |
|-------|-------|
| Viewport A | Common desktop width (e.g. 1440px) |
| Viewport B | Narrow/mobile-ish width supported by the app |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | At Viewport A, render the chip list with one or more attached files present in the composer | Chip list, attachments area, message input, model selector, and send button all remain fully visible with no overlap |
| 2 | At Viewport A, resize slightly and observe wrapping/spacing of the chip list | Chip list wraps or scrolls gracefully without covering adjacent composer elements |
| 3 | Resize to Viewport B and repeat steps 1–2 | No overlap occurs at the narrow width either; chip list adapts (wraps/scrolls/collapses) as needed |

---

## Expected Final State

The chip list is laid out so that it never visually collides with any other composer-area control, at any supported viewport width.

---

## Pass/Fail Criteria

**Pass:**
- No visual overlap between the chip list and the input, attachments area, model selector, or send button at either viewport.

**Fail:**
- The chip list overlaps or obscures any of the listed composer elements at either viewport width.
