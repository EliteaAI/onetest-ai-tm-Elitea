---
id: ELITEA-2823
title: "Chat – Follow-Up Suggestion Chips Support Keyboard Navigation and Correct Focus/Hover/Selected States"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:chat, issue:6254]
requirements: [EliteaAI/elitea_issues#6254]
---

# ELITEA-2823: Chat – Follow-Up Suggestion Chips Support Keyboard Navigation and Correct Focus/Hover/Selected States

**Module:** chat-interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify chips can be navigated and selected via keyboard, and that visible focus, hover, and selected states render correctly in both light and dark theme.

---

## Preconditions

- Follow-up suggestions feature flag is ON globally and the current project is not on the disallow-list.
- A suggestion-eligible AI response has rendered at least 3 chips.
- Ability to switch between light and dark theme.

---

## Test Data

| Field | Value |
|-------|-------|
| Theme A | Light theme |
| Theme B | Dark theme |

---

## Steps

| # | Action | Expected Result |
|---|--------|--------------------|
| 1 | Using only the keyboard, move focus into the chip list (e.g. Tab) | A chip receives visible keyboard focus |
| 2 | Use arrow keys to move between chips | Focus moves between chips per the documented arrow-key pattern |
| 3 | Press Enter or Space on a focused chip | The focused chip's action fires (text inserted into input), identical to a mouse click |
| 4 | Hover a chip with the mouse (no click) | A visible hover state renders, distinct from the default/idle chip appearance |
| 5 | Click a chip so it becomes the current selection, then check for a visible selected-state indicator while it remains visible | Selected chip is visually distinguished from unselected chips |
| 6 | Repeat steps 1, 4, and 5 in Theme B (dark theme) | Focus, hover, and selected states remain clearly visible and match the Figma spec for dark theme |

---

## Expected Final State

Chips are fully operable via keyboard, and all interaction states (focus, hover, selected) are visually correct in both themes.

---

## Pass/Fail Criteria

**Pass:**
- Keyboard focus, arrow navigation, and Enter/Space activation all work as expected.
- Hover and selected states are visually distinct in both light and dark theme.

**Fail:**
- Chips are not keyboard-focusable or arrow-navigable.
- Enter/Space does not activate a focused chip.
- Focus, hover, or selected state is missing/indistinguishable in either theme.
