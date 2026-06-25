---
id: ELITEA-0624
title: "Support Assistant expands to full-view mode and collapses back to widget mode"
priority: high
type: functional
module: elitea-chat-bot
status: ready
execution_type: automated
automation_test_id:
  - test_support_assistant_smoke.py:TestSupportAssistantSmoke.test_expand_collapse_fullview
tags: [expand-collapse, display-modes, story:4774, full-view, r-2.0.3, widget]
requirements: [4774]
---
# ELITEA-0624: Support Assistant expands to full-view mode and collapses back to widget mode

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify the two display modes of the Support Assistant: compact widget mode (floating panel) and full-view mode (expanded overlay). Expanding must not lose conversation content. Collapsing must return the user to widget mode with all content intact. All features must be functional in both modes.

## Preconditions

Support Assistant is enabled.
The panel is open in widget/compact mode with at least one message sent and response received.

## Test Data

Any test message (e.g., "Explain how to create an agent")

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | With the panel open in widget mode, locate the expand button (maximize icon or equivalent) | Expand button is visible within the panel header or controls area |
| 2 | Click the expand button | Panel transitions to full-view mode; all previous messages are still visible |
| 3 | In full-view mode, send a new message | Message is sent; assistant response is received in full-view mode |
| 4 | Locate the collapse/minimize button in full-view mode | Collapse button is visible |
| 5 | Click the collapse button | Panel returns to widget/compact mode; all messages (including the one sent in step 3) are still visible |
| 6 | Verify the launcher icon/button is back to its normal resting position | Launcher is not affected by the mode transition |

## Expected Final State

Launcher is not affected by the mode transition

## Pass/Fail Criteria

PASS: Expand transitions to full-view; collapse returns to widget; all messages present in both modes; no content loss or flash.
FAIL: Expand or collapse button missing; messages lost during transition; panel freezes or resets.
