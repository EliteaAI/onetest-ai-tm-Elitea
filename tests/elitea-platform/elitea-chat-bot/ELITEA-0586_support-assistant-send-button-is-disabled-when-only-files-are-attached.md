---
id: ELITEA-0586
title: "Support Assistant — Send Button Is Disabled When Only Files Are Attached and Text Input Is Empty"
priority: critical
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0586: Support Assistant — Send Button Is Disabled When Only Files Are Attached and Text Input Is Empty

**Module:** Elitea Chat Bot · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that attaching a file to the Support Assistant composer without typing any text keeps the Send button disabled, and the button only becomes enabled when text is also present.

**Coverage:**
- Send button disabled when only file attached, no text
- Send button enables when text is added alongside attachment
- Send button reverts to disabled when text is cleared
- Enter key also does not submit without text

## Preconditions

- Logged into {{base_url}} as a regular user
- Support Assistant is enabled by admin
- Browser: Chrome/Edge (latest)

## Test Data

image.png (< 1 MB)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Support Assistant widget. Observe the Send button in its initial state. | Send button is disabled (grayed out / non-clickable). Composer is empty. |
| 2 | Click the paperclip icon and attach image.png | File thumbnail appears in compose area. Send button remains disabled. |
| 3 | Attempt to click the Send button | Button is not clickable; no message is sent |
| 4 | Press Enter on the keyboard | No message is sent; Enter does not trigger submission |
| 5 | Type "Please review this file." in the text input | Text appears in the composer. Send button becomes enabled (active/highlighted). |
| 6 | Clear the typed text (delete all characters) | Send button returns to disabled state. Attachment thumbnail is still present. |
| 7 | Type one character in the text input | Send button becomes enabled again |
| 8 | Click Send | Message with the attachment and text is submitted successfully. Bot responds. |

## Expected Final State

Message with the attachment and text is submitted successfully. Bot responds.

## Pass/Fail Criteria

**Pass:**
- Send button is disabled when only a file is attached with no text
- Enter key does not submit without text
- Send button enables immediately when text is added
- Send button disables again when text is cleared

**Fail:**
- Send button is enabled with file attached but no text
- Pressing Enter submits an empty-text + file message
- Send button does not enable even after text is typed
- Attachment is lost when text is typed or cleared
