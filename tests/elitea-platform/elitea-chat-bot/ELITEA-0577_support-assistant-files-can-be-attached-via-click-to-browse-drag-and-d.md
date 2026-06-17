---
id: ELITEA-0577
title: "Support Assistant — Files Can Be Attached via Click-to-Browse, Drag-and-Drop, and Clipboard Paste"
priority: critical
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0577: Support Assistant — Files Can Be Attached via Click-to-Browse, Drag-and-Drop, and Clipboard Paste

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that all three upload methods (click-to-browse, drag-and-drop, and Ctrl+V paste) work correctly in the Support Assistant composer.

**Coverage:**
- Click-to-browse via paperclip icon attaches file and shows thumbnail
- Drag-and-drop from OS file explorer onto compose area attaches file
- Clipboard paste (Ctrl+V) for images attaches image from clipboard
- Counter decrements correctly for each method

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)
- Test files on desktop: image1.png (< 1 MB), image2.jpg (< 1 MB)
- A screenshot image copied to Windows clipboard (via Snipping Tool)

## Test Data

- image1.png (< 1 MB) — for drag-and-drop
- image2.jpg (< 1 MB) — for click-to-browse
- Windows clipboard image (captured via Snipping Tool) — for paste

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget | Widget opens with empty composer |
| 2 | Method 1 – Click to Browse: Click the paperclip icon. In the file browser, select image2.jpg. | image2.jpg thumbnail appears in compose area. Counter shows "Attach files (9 left)". |
| 3 | Remove image2.jpg by clicking the X on its thumbnail | Thumbnail removed. Counter resets to "10 left". |
| 4 | Method 2 – Drag and Drop: Open OS file explorer. Drag image1.png from desktop and drop it onto the Support Assistant message composer area. | image1.png is attached. Thumbnail appears. Counter shows "9 left". |
| 5 | Remove image1.png by clicking the X on its thumbnail | Thumbnail removed. Counter resets to "10 left". |
| 6 | Method 3 – Clipboard Paste: Open Snipping Tool and capture a screenshot (it goes to clipboard). Click inside the Support Assistant text input. Press Ctrl+V. | Clipboard image is attached as a file. Thumbnail appears in compose area. Counter shows "9 left". |
| 7 | Type "Please review this image." and click Send | Message with the pasted image is sent. Bot responds. No errors. |

## Expected Final State

Message with the pasted image is sent. Bot responds. No errors.

## Pass/Fail Criteria

**Pass:**
- All three methods successfully add attachment thumbnails to the compose area
- Counter decrements correctly for each method
- Sending with any method produces a bot response without errors

**Fail:**
- Any one method fails to attach a file
- Drag-and-drop zone is not recognized (no drop feedback, file not attached)
- Ctrl+V paste has no effect in the composer
- Counter does not update after attachment
