---
id: ELITEA-3241
title: "Input only resizes via manual drag (hover shows resize cursor) between min and max height, in both compact and full-view modes; typing never auto-grows it; Enter/Shift+Enter/Ctrl+Enter/Cmd+Enter behave correctly"
priority: critical
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6, eng:design, eng:frontend, nfr:usability]
requirements: [EliteaAI/elitea_issues#5197]
---

# ELITEA-3241: Input only resizes via manual drag between min and max height; typing never auto-grows it

**Module:** elitea-chat-bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Support Assistant chat input's height changes only through a manual hover-and-drag on its resize line, bounded by a mode-specific minimum and maximum, and never grows or shrinks from typing alone — in both compact and full-view modes. Also verify that only a plain Enter key sends the message; Shift+Enter, Ctrl+Enter, and Cmd+Enter must not.

**Coverage:**
- Typing long text without Enter never changes the field's height (text auto-scrolls instead)
- Hovering the resize line shows a resize/expand cursor
- Dragging the resize line up/down is bounded by the mode's min and max height
- Typing at minimum height still does not resize the field
- Shift+Enter inserts a line break without sending
- Ctrl+Enter and Cmd+Enter do not send
- Plain Enter sends and resets the field to its default rest height
- All of the above hold in both compact popup and full-view mode

## Preconditions
- User is logged in to `{{base_url}}`
- Support Assistant is enabled

## Test Data
| Field | Value |
|---|---|
| Long text | Any text long enough to wrap across 10+ lines when typed continuously (no Enter key) |

## Steps
| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Support Assistant chat (compact popup) | Widget opens with the input at its default rest height |
| 2 | Type the long text, without pressing Enter, until it would need several lines | |
| 3 | Keep typing past the point where the visible area is full | The text automatically scrolls up so the line you're typing stays visible; the field's height itself is unchanged |
| 4 | Move the mouse to the top edge/line of the input, without clicking | Cursor changes to a resize/expand indicator |
| 5 | Click and drag that line upward as far as it will go | Field grows to the compact-mode maximum (about 6-8 lines) and stops there, even if you keep dragging |
| 6 | Click and drag that line downward as far as it will go | Field shrinks to its minimum usable height and stops there |
| 7 | At that minimum height, type text longer than fits | Field stays at that fixed height; text auto-scrolls up; enables you to scroll; height still doesn't change from typing |
| 8 | Type "Line one", press Shift+Enter, type "Line two", press Shift+Enter, type "Line three" | No message is sent; all three lines appear in the field |
| 9 | Press Ctrl+Enter | Message is NOT sent |
| 10 | Press Cmd+Enter (or its OS equivalent) | Message is NOT sent |
| 11 | Press Enter with no modifier key | Message sends with the line breaks preserved; field returns to its default rest height |
| 12 | Click Expand to open full-view mode | Widget switches to full-view |
| 13 | Repeat steps 4-6 in full-view mode | Field can be dragged between the same minimum and a taller full-view maximum (about 12-14 lines); typing alone still does not change its height |
| 14 | Repeat steps 8-11 in full-view mode | Same result as compact mode: only plain Enter sends |

## Expected Final State
The chat is open in full-view mode, the input is back at its default rest height, and the last message sent (from step 14's Enter) is visible at the bottom of the message list.

## Pass/Fail Criteria
**Pass:**
- Height changes only when the user drags the resize line, never from typing alone, in either mode
- Drag is correctly bounded between the minimum and each mode's maximum
- No scrollbar ever appears (text auto-scrolls instead)
- Only plain Enter sends the message; Shift+Enter/Ctrl+Enter/Cmd+Enter do not

**Fail:**
- Typing alone changes the field's height
- Dragging goes past the expected min/max for the current mode
- A scrollbar appears
- Any Enter-key combination behaves incorrectly (wrong key sends, or plain Enter fails to send)
