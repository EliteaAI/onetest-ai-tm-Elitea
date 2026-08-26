---
id: ELITEA-2820
title: "Chat – Follow-Up Suggestion Chip List Rendering Rules (Max 3, No Empty Chips, Truncation)"
priority: high
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6254]
requirements: [EliteaAI/elitea_issues#6254]
---

# ELITEA-2820: Chat – Follow-Up Suggestion Chip List Rendering Rules (Max 3, No Empty Chips, Truncation)

**Module:** chat-interface · **Priority:** High · **Type:** Functional

**Objective:** Verify the chip list renders as separate clickable chips above the composer (not merged/inline), shows at most 3 chips even if the backend returns more, never renders empty/blank chips, and truncates long text while keeping the full text accessible.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- Ability to control/observe the backend suggestion response (e.g. via network inspection or a test hook returning more than 3 suggestions, including a blank one).

---

## Test Data

| Field | Value |
|-------|-------|
| Backend response A | 5 non-empty suggestions of varying length, one of them very long |
| Backend response B | A response set including at least one empty/blank suggestion string |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Trigger a suggestion-eligible response with Backend response A | Chip list renders as distinct clickable chip elements above the composer, not as one merged block or inline text |
| 2 | Count the rendered chips | Exactly 3 chips are shown even though 5 were returned |
| 3 | Locate the chip containing the very long suggestion | Text is visually truncated within the chip |
| 4 | Hover or focus the truncated chip (or open its expanded view per implementation) | Full suggestion text is available via tooltip/accessible label/expanded view |
| 5 | Trigger a suggestion-eligible response with Backend response B | No chip is rendered for the empty/blank suggestion entry |

---

## Expected Final State

The chip list always respects the 3-chip cap, never renders blank chips, and never loses information for long suggestions due to truncation.

---

## Pass/Fail Criteria

**Pass:**
- At most 3 chips render regardless of backend count.
- No empty/blank chip is ever rendered.
- Truncated text remains fully accessible via tooltip/label/expanded view.

**Fail:**
- More than 3 chips render.
- An empty/blank chip renders.
- Truncated text has no way to be read in full.
