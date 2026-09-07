---
id: ELITEA-3242
title: "Manually-set input height stays correct across mode switches, file attachments, and the widget's lifecycle (close/reopen, navigation, refresh); message list stays usable at max height"
priority: critical
type: regression
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, eng:design, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#5197]
---

# ELITEA-3242: Manually-set input height persists correctly across mode switches, attachments, and widget lifecycle

**Module:** elitea-chat-bot · **Priority:** Critical · **Type:** Regression

**Objective:** Verify that a manually-set input height introduced by the new drag-to-resize behavior does not break other chat-bot functionality: the message list stays usable when the input is at its maximum height, a mode switch doesn't leave the input in a broken state, the resize handle and file-attachment chip don't interfere with each other, and the height doesn't get stuck in an abnormal state across close/reopen, page navigation, or a page refresh.

**Coverage:**
- Message list remains at least partly visible/scrollable when the input is at max height
- Input height stays sensible when switching between compact and full-view mode
- Resize handle and attached-file chip do not block each other
- Input height returns to a normal, usable state after close/reopen
- Input height returns to a normal, usable state after in-app navigation
- Input height returns to a normal, usable state after a page refresh

## Preconditions
- User is logged in to `{{base_url}}`
- Support Assistant is enabled
- At least 2-3 messages already exist in the conversation
- One small file available to attach (e.g. image.png, under 1MB)

## Test Data
| Field | Value |
|---|---|
| Attachment | image.png (under 1MB) |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Support Assistant chat (compact popup) with prior messages visible | Widget opens showing the existing conversation |
| 2 | Drag the resize line to grow the input to its maximum compact height | The message list above shrinks but stays at least partly visible and scrollable — it is never fully hidden |
| 3 | Click Expand to switch to full-view mode | Input keeps a sensible height in full-view — it does not break or jump unexpectedly |
| 4 | Drag the resize line in full-view mode to a height taller than the compact-mode maximum, but still within the full-view maximum | Field grows to that height and stops there |
| 5 | Attach the test file | A file chip appears above the input |
| 6 | Hover and drag the resize line near the file chip | The chip's remove button still works; the resize drag still works; neither blocks the other |
| 7 | Resize the input to a custom height, then close the widget and reopen it | Input returns to a normal, usable height — not stuck at zero or an oversized state |
| 8 | Resize the input, then navigate to a different page in the app and come back | Input is still at a normal, usable height |
| 9 | Resize the input, then refresh the page | Input is still at a normal, usable height |

## Expected Final State
The chat widget is open with the input at a normal, usable height, no leftover file chip from the earlier attachment, and the existing conversation history is intact and visible.

## Pass/Fail Criteria
**Pass:**
- Message list stays usable (at least partly visible and scrollable) at max input height
- Height stays sensible across a mode switch (no break or jump)
- The attachment chip and resize handle never interfere with each other
- Height returns to normal after close/reopen, after navigation, and after a page refresh

**Fail:**
- Message list becomes fully hidden at max input height
- Input height breaks, jumps, or overflows on a mode switch
- The resize handle and attachment chip block each other's interaction
- Input renders broken (zero-height, oversized, off-screen) after close/reopen, navigation, or refresh
