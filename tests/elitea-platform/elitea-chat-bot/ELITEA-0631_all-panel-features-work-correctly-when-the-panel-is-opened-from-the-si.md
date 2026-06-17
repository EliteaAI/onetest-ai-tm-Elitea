---
id: ELITEA-0631
title: "All panel features work correctly when the panel is opened from the sidebar entry"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: manual
tags: [feature-parity, sidebar, smoke]
requirements: [#4780]
---
# ELITEA-0631: All panel features work correctly when the panel is opened from the sidebar entry

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Opening the Support Assistant from the sidebar entry must provide a fully functional experience identical to opening it from the floating launcher. Any feature that breaks specifically after a sidebar-launch is a placement-specific defect.

## Preconditions

Logged in to ELITEA ({{base_url}}
Support Assistant feature is enabled

## Test Data

Message to send: "Hello, testing from sidebar"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the "Support Assistant" entry at the bottom of the sidebar. | The Support Assistant panel opens. |
| 2 | Type "Hello, testing from sidebar" in the message input and send it by clicking Send. | Message appears in the conversation as a user message. The assistant responds. |
| 3 | Click the Chat History button in the panel header. | A list of previous sessions appears (or an empty state if no prior sessions exist). |
| 4 | Click the New Chat button in the panel header. | A clean new session opens with the welcome message. The previous session moves to history. |
| 5 | Click the Attach File button in the message input area. | A file picker dialog opens or the attachment UI appears. |
| 6 | Click the Expand button in the panel header. | The panel expands to a larger full-view overlay. |
| 7 | Click the Expand/collapse button again while in full view. | The panel returns to compact widget mode. |
| 8 | Click the X (Close) button. | The panel closes. The sidebar entry and launcher are both still visible. |

## Expected Final State

The panel closes. The sidebar entry and launcher are both still visible.

## Pass/Fail Criteria

Pass: All actions in steps 2–8 work correctly after opening the panel from the sidebar entry; No feature is missing or broken compared to opening from the floating launcher.
Fail: Any step fails specifically after a sidebar-launched open; The panel opened from the sidebar is missing buttons or features; Closing the panel removes the sidebar entry from the navigation.
