---
id: ELITEA-0587
title: "Support Assistant — Attach Button Behaves Correctly Across All Five Composer States"
priority: critical
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0587: Support Assistant — Attach Button Behaves Correctly Across All Five Composer States

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the attach files button behaves correctly across all Support Assistant composer states: open (empty), enter request (typing), send request (generating response), full view, and after receiving a response.

**Coverage:**
- Open state: attach button is interactive
- Enter request state: attach button remains interactive while typing
- Send request / generating response state: attach button is disabled during generation
- Full view expanded state: attach button is interactive
- After response received: attach button is interactive again

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)

## Test Data

image.png (< 1 MB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open state: Open the Support Assistant widget. Observe the composer with no text and no attachments. | Paperclip icon is visible and interactive. Hovering shows "Attach files (10 left)". |
| 2 | Click the paperclip. Select image.png. | File attached. Thumbnail visible. |
| 3 | Remove the attachment (click X on thumbnail). | Thumbnail removed. Counter resets to 10. |
| 4 | Enter request state: Type "Please review this." in the text input (do NOT send yet). | Text appears in composer. |
| 5 | Click the paperclip while text is already typed. Select image.png. | File attaches alongside the text. Thumbnail visible. |
| 6 | Send request state: Click Send (with text and attachment). While the bot is generating (loading indicator visible), observe the paperclip icon. | Paperclip icon is disabled during generation. No new attachment can be started. |
| 7 | Wait for the bot response to complete. | Bot response appears. Paperclip icon becomes active/interactive again. |
| 8 | Full view state: Click the expand icon to switch to full view mode. Observe the composer. | Paperclip icon is visible and interactive in full view mode. |
| 9 | Click the paperclip in full view. Select image.png. Type a message. Click Send. | File attaches in full view. Message sent. Bot responds. |

## Expected Final State

File attaches in full view. Message sent. Bot responds.

## Pass/Fail Criteria

**Pass:**
- Paperclip is interactive in: open, enter request, full view, and after-response states
- Paperclip is disabled during bot response generation
- No errors in any state transition

**Fail:**
- Paperclip is disabled/non-functional in the open or enter request state
- Paperclip remains active during response generation
- Attachment is lost when switching from compact to full view before sending
- Error or crash on any state transition
