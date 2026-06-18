---
id: ELITEA-0583
title: "Support Assistant — Multiple Clipboard-Pasted Images With Duplicate Names Are Handled Gracefully"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0583: Support Assistant — Multiple Clipboard-Pasted Images With Duplicate Names Are Handled Gracefully

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that pasting multiple images from the Windows clipboard (e.g., repeated screenshots from Snipping Tool, all auto-named "image.png") does not crash the composer, and duplicate filenames are resolved automatically.

**Coverage:**
- First clipboard paste attaches image successfully
- Second clipboard paste with same auto-generated name is accepted without error
- Duplicate names are auto-renamed with a distinguishing suffix
- All pasted images are visible as separate thumbnails
- Sending with multiple pasted images produces a bot response

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest, Windows)
- Windows Snipping Tool available

## Test Data

- Clipboard image 1: screenshot captured via Windows Snipping Tool (auto-named "image.png")
- Clipboard image 2: a second screenshot captured via Windows Snipping Tool (auto-named "image.png" — same name, different content)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget | Empty composer |
| 2 | Capture a screenshot with Windows Snipping Tool (image on clipboard). Click inside Support Assistant text input. Press Ctrl+V. | First image attached. Thumbnail appears. Counter shows "9 left". |
| 3 | Capture a second different screenshot with Snipping Tool (clipboard updated). Press Ctrl+V in the text input again. | Second image attached WITHOUT error. Its filename is auto-renamed (e.g., "image_20260522_143022_1.50KB.png"). Counter shows "8 left". |
| 4 | Confirm both thumbnails are visible as separate, distinct attachments with different names | Two separate thumbnails with distinguishable names/identifiers |
| 5 | Type "Please review these two screenshots." and click Send | Both images sent with the message. Bot responds. No errors or crashes. |

## Expected Final State

Both images sent with the message. Bot responds. No errors or crashes.

## Pass/Fail Criteria

**Pass:**
- Both pasted images are attached without error
- Duplicate filename is auto-renamed with a suffix
- Both thumbnails appear as separate distinct items
- Both images are sent with the message

**Fail:**
- Second paste fails with an error ("Duplicate file name" or similar)
- Only one of the two images is attached (second overwrites or is rejected)
- Both show identical names (duplicate not resolved)
- Widget crashes or becomes unresponsive after second paste
