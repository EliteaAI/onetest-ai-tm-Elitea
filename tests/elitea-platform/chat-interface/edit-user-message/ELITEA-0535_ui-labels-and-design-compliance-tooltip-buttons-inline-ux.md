---
id: ELITEA-0535
title: "UI labels and design compliance — tooltip, buttons, inline UX"
priority: medium
type: functional
module: edit-user-message
status: ready
execution_type: manual
tags: [feat:chat, r-2.0.4]
requirements: [EliteaAI/elitea_issues#4942]
---
# ELITEA-0535: UI labels and design compliance — tooltip, buttons, inline UX

**Module:** Edit User Message · **Priority:** Medium · **Type:** Functional

**Objective:** Verify all UI labels, placements, and visual behaviors match the design specification.

**Coverage:**
- Tooltip = "Edit"
- Button labels = "Cancel" and "Save and apply"
- No modal/redirect on edit
- No visual regressions on non-edited messages

## Preconditions

- User is logged in to ELITEA at {{base_url}}
- Browser: Chrome latest
- A conversation with at least 2 user-assistant exchanges

## Test Data

- Any existing conversation

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Hover over the Edit icon on the last user message. | Tooltip text reads exactly "Edit the message and regenerate answer". |
| 2 | Click the Edit icon. Verify button labels. | Buttons read exactly "Cancel" and "Save and apply" (check casing and spacing). |
| 3 | Verify the position of the buttons. | Both buttons are at the bottom-right of the editable message area. |
| 4 | While in edit mode, check other messages in the conversation for visual regressions. | Non-edited messages display normally — no layout shifts, styling changes, or missing elements. |
| 5 | Click Cancel. Verify the message returns to the standard ELITEA chat design. | Message returns to read-only view consistent with the ELITEA chat visual style. |

## Expected Final State

Message returns to read-only view consistent with the ELITEA chat visual style.

## Pass/Fail Criteria

**Pass:**
- All labels match exactly
- Button placement is bottom-right
- No visual regressions
- Inline edit matches ELITEA design system

**Fail:**
- Incorrect label text or casing
- Buttons in wrong position
- Visual regressions on other messages
- Styling inconsistent with ELITEA design
