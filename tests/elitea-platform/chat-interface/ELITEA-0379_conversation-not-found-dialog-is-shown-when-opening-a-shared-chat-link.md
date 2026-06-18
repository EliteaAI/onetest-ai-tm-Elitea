---
id: ELITEA-0379
title: "\"Conversation not found\" dialog is shown when opening a shared chat link without access"
priority: medium
type: functional
module: chat-interface
status: draft
execution_type: manual
tags: [nfr:usability, eng:frontend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4374]
---
# ELITEA-0379: "Conversation not found" dialog is shown when opening a shared chat link without access

**Module:** Chat Interface · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that a user who opens a shared conversation URL for a conversation they cannot access sees the "Conversation not found" dialog instead of being silently redirected to a new empty chat.

**Coverage:**
- Dialog title "Conversation not found" is displayed
- Dialog message is generic and contains no sensitive conversation data
- "Got it" button is present and dismisses the dialog
- User is redirected to their last available conversation after clicking "Got it"
- URL updates to reflect the redirected conversation (no longer points to the inaccessible ID)
- Old behavior (silent redirect to new empty chat with no explanation) does NOT occur

## Preconditions

- Logged in as User B (a team project member who does NOT have access to User A's non-public conversation)
- User A has created a non-public (private) conversation in a team project and shared its URL
- User B is a member of the same team project but the conversation is not shared with them
- User B has at least one conversation of their own
- Environment: {{base_url}}

## Test Data

- Inaccessible shared conversation URL: {{base_url}}
- Non-existent conversation ID variant: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Log in as User B | User B is on the Chat page in their own project |
| 2 | Paste the inaccessible conversation URL into the browser address bar and navigate to it | Page begins loading; URL stays at the inaccessible conversation ID |
| 3 | Wait 2–3 seconds for the page to settle | A dialog with the title "Conversation not found" appears |
| 4 | Read the dialog message | Message reads: "The conversation you are looking for does not exist in your project or you don't have access to it." — no private conversation name, message content, or participant data is visible |
| 5 | Click the "Got it" button | Dialog disappears |
| 6 | Observe the page and address bar after redirect | User is taken to their last active conversation; URL no longer contains the invalid conversation ID |
| 7 | Attempt to type and send a message in the redirected conversation | Chat history is visible; message input is available; message sends successfully |

## Expected Final State

Chat history is visible; message input is available; message sends successfully

## Pass/Fail Criteria

**Pass:**
- "Conversation not found" dialog appears within 3 seconds of navigating to the inaccessible URL
- Dialog message contains no sensitive data from the target conversation
- "Got it" redirects to a valid conversation and URL updates correctly
- No crash or blank screen at any point

**Fail:**
- User is silently redirected to a new empty chat with no dialog
- Dialog does not appear or is missing the "Got it" button
- Dialog reveals the conversation name, messages, or participant names
- URL still points to the invalid conversation ID after redirect
- Any crash or white screen occurs
