---
id: ELITEA-0994
title: "Keyboard Navigation in Authorization Dialog"
priority: medium
type: functional
module: sensitive-tool-calling
status: ready
execution_type: manual
tags: [user_story:3780, feat:agents, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3780]
---
# ELITEA-0994: Keyboard Navigation in Authorization Dialog

**Module:** Sensitive Tool Calling · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the authorization dialog supports keyboard navigation — the Parameters accordion can be toggled via keyboard, and the Authorize/Block buttons are reachable and activatable via Tab and Enter/Space.

## Preconditions

- Authorization dialog is currently displayed in the chat

## Test Data

- Keyboard keys used: Tab (cycle focus), Enter/Space (activate)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | When the dialog is open, press Tab to cycle through focusable elements. | Focus cycles through interactive elements in the dialog (Parameters header, Authorize button, Block button). |
| 2 | When focus is on the Parameters accordion header, press Enter or Space. | Parameters section toggles (collapses if open, expands if closed). |
| 3 | Tab to the [Authorize] button. Press Enter or Space. | [Authorize] action is triggered. Dialog closes and tool executes. |
| 4 | Trigger the dialog again. Tab to the [Block] button. Press Enter or Space. | [Block] action is triggered. Dialog closes and tool is blocked. |

## Expected Final State

[Block] action is triggered. Dialog closes and tool is blocked.

## Pass/Fail Criteria

Pass:
- All dialog interactive elements are reachable via Tab
- Parameters accordion toggles with Enter or Space when focused
- Authorize and Block can be activated via keyboard

Fail:
- Tab focus does not enter the dialog
- Parameters accordion not keyboard-accessible
- Authorize or Block cannot be activated via keyboard
