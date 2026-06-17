---
id: ELITEA-0574
title: "Support Assistant Composer Shows Attach Button with Correct Counter in All Widget Entry Points"
priority: critical
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0574: Support Assistant Composer Shows Attach Button with Correct Counter in All Widget Entry Points

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the attach files (paperclip) icon is visible in the Support Assistant composer, clickable, and displays the correct "N files left" counter tooltip.

**Coverage:**
- Attach button visibility in both compact widget and full-view modes
- File browser opens on click
- Tooltip shows "Attach files (10 left)" when no files are attached
- Button is interactive in both compact and full view

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin (Admin → Guardrails → toggle ON)
- Browser: Chrome/Edge (latest)

## Test Data

image.png (< 1 MB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to {{base_url}} | Floating Support Assistant launcher (circular button) is visible in the bottom-right corner |
| 2 | Click the floating launcher to open the widget in compact mode | Widget opens; composer/input area is visible at the bottom |
| 3 | Observe the composer toolbar | A paperclip (attach files) icon is visible in the composer toolbar |
| 4 | Hover over the paperclip icon (do not click) | Tooltip reads "Attach files (10 left)" |
| 5 | Click the paperclip icon | OS file browser dialog opens. No error or crash. |
| 6 | Cancel/dismiss the file browser | File browser closes; composer returns to normal state |
| 7 | Click the expand icon to switch to full-view mode | Widget expands to full view |
| 8 | Observe the composer in full-view mode | Paperclip icon is present in the composer in full view as well |
| 9 | Click the paperclip icon in full-view mode | File browser opens. No error or crash. |

## Expected Final State

File browser opens. No error or crash.

## Pass/Fail Criteria

**Pass:**
- Paperclip icon is present in both compact and full-view modes
- Hovering shows "Attach files (10 left)"
- Clicking opens OS file browser
- No errors, no crashes

**Fail:**
- Paperclip icon is absent or invisible
- Tooltip is missing, blank, or shows incorrect count
- Clicking paperclip triggers an error or does not open file browser
- Icon is present but non-interactive
