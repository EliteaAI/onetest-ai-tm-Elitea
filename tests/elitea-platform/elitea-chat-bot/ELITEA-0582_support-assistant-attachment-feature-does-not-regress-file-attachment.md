---
id: ELITEA-0582
title: "Support Assistant Attachment Feature Does Not Regress File Attachment in Regular Chat Conversations"
priority: high
type: functional
module: elitea-chat-bot
status: draft
execution_type: manual
tags: [user_story:4777, r-2.0.3, 4777]
requirements: [EliteaAI/elitea_issues#4777]
---
# ELITEA-0582: Support Assistant Attachment Feature Does Not Regress File Attachment in Regular Chat Conversations

**Module:** Elitea Chat Bot · **Priority:** High · **Type:** Functional

**Objective:** Verify that the implementation of the Support Assistant attachment feature does not break the existing file attachment functionality in regular private chat conversations.

**Coverage:**
- Attach button is present and functional in regular Chat composer
- File attaches and thumbnail shown in regular Chat compose area
- Sending with attachment in regular Chat produces a bot response (no socket error)
- Attached file is stored in the Artifacts attachments bucket

## Preconditions

- Logged into {{base_url}} as a regular user
- An active private project with Chat access (e.g., project "Private")
- Browser: Chrome/Edge (latest)

## Test Data

- Project: Private (or any active project with an LLM agent configured)
- image.png (< 1 MB)
- Artifacts bucket: attachments

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to https://next.elitea.ai/app/ and select a project from the sidebar dropdown (e.g., "Private") | Project selected. Chat page opens. |
| 2 | Navigate to Chat in the sidebar | Regular Chat composer is visible (not the Support Assistant widget) |
| 3 | Observe the composer area | Paperclip/attach icon is visible in the regular Chat composer toolbar |
| 4 | Click the paperclip icon | OS file browser opens |
| 5 | Select image.png | File attached; thumbnail appears in the regular Chat compose area |
| 6 | Type "Please describe this image." in the text input | Text and attachment thumbnail both visible |
| 7 | Click Send | Message sent. Bot responds with a description of the image. No socket errors. No blank response. |
| 8 | Navigate to Artifacts in the sidebar. Open the "attachments" bucket. | image.png (or a renamed version) is present in the attachments bucket. |

## Expected Final State

image.png (or a renamed version) is present in the attachments bucket.

## Pass/Fail Criteria

**Pass:**
- Regular Chat attach button is present and functional
- File attaches and thumbnail shown in regular Chat compose area
- Bot responds successfully after sending message with attachment
- Attached file is stored in Artifacts attachments bucket

**Fail:**
- Attach button missing or non-functional in regular Chat after Support Assistant feature deployment
- Sending file attachment in regular Chat causes socket error
- No bot response received with attachment in regular Chat
- File is not stored in Artifacts
