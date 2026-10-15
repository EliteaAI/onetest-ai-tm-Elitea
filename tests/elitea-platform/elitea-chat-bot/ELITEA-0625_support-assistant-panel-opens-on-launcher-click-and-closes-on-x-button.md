---
id: ELITEA-0625
title: "Support Assistant panel opens on launcher click and closes on X button click"
priority: critical
type: functional
module: elitea-chat-bot
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.support_assistant.test_support_assistant_smoke.TestSupportAssistantLauncher.test_launcher_visible_and_opens_widget
tags: [open-close, story:4774, lifecycle, launcher, r-2.0.3, smoke]
requirements: [4774]
---
# ELITEA-0625: Support Assistant panel opens on launcher click and closes on X button click

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the complete open/close lifecycle of the Support Assistant panel: clicking the floating launcher opens the widget panel; clicking the close (X) button dismisses it; re-opening the launcher restores the same panel without losing conversation state.

## Preconditions

Support Assistant is enabled by admin.
Tester is logged in as a regular user.
The Support Assistant has not been opened in this session yet.

## Test Data

Any test message (e.g., "Hello")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the floating launcher icon | The Support Assistant panel opens in widget/compact mode; welcome message or empty composer is shown |
| 2 | Type "Hello" in the message composer and send it | Message is sent; assistant response is received |
| 3 | Click the X (close) button on the Support Assistant panel | The panel closes; the floating launcher returns to its resting state |
| 4 | Click the floating launcher icon again | The panel reopens; "Hello" and the assistant response are still visible |
| 5 | Click the X button again | Panel closes cleanly |

## Expected Final State

Panel closes cleanly

## Pass/Fail Criteria

PASS: Panel opens on launcher click, closes on X click, conversation is intact on reopen.
FAIL: Panel fails to open, fails to close, or messages are lost after close/reopen.
