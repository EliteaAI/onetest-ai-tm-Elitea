---
id: ELITEA-0891
title: "Paperclip Icon Becomes Inactive When Selecting Pipeline With Allow Attachments OFF as Main Participant in Existing Chat"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:pipelines, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5030]
---
# ELITEA-0891: Paperclip Icon Becomes Inactive When Selecting Pipeline With Allow Attachments OFF as Main Participant in Existing Chat

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that the paperclip icon in the chat message input area correctly reflects inactive state when a pipeline with Allow Attachments OFF is selected as the main acting participant in an existing chat that already has messages.

**Coverage:**
- Existing chat session (1+ messages already sent)
- Adding a pipeline with Allow Attachments OFF to the participants list does NOT automatically change the paperclip state (pipeline does not substitute the default chat model automatically)
- Paperclip icon becomes inactive only after the user explicitly selects the pipeline as the main acting unit
- No false-positive active state retained after the pipeline is made the active participant

## Preconditions

- Logged in to {{base_url}}
- A pipeline exists with Allow Attachments toggle set to OFF
- An existing chat conversation with at least 1 sent message is available
- The existing chat does NOT already have the test pipeline as a participant

## Test Data

- Pipeline: any pipeline with Allow Attachments OFF (e.g., name "Attachments pipeline")
- Existing chat: a conversation with at least 1 human/AI message exchange
- Environment: {{base_url}}
- Browser: Chrome latest

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open an existing chat conversation that already contains at least one message | Chat history is visible; the message input area is available |
| 2 | Observe the paperclip icon state in the message input area before adding any pipeline | Note the current icon state for comparison (active or inactive based on prior chat configuration) |
| 3 | Open the Participants panel and add the pipeline (with Allow Attachments OFF) as a participant — do NOT select it as the main acting unit yet | Pipeline appears in the Participants list; the default chat model is still the active acting unit; paperclip icon state is unchanged at this point |
| 4 | Select the pipeline as the main acting unit (e.g., click the pipeline to make it the primary/active participant for the conversation) | Pipeline is now the active acting participant for the conversation |
| 5 | Observe the paperclip icon in the chat message input area immediately after selecting the pipeline as the main participant | Paperclip icon is inactive (greyed out / not clickable), reflecting that the active participant has Allow Attachments disabled |
| 6 | Attempt to click the inactive paperclip icon | No file attachment dialog opens; the icon does not respond as if attachments are enabled |

## Expected Final State

No file attachment dialog opens; the icon does not respond as if attachments are enabled

## Pass/Fail Criteria

**Pass:**
- Paperclip icon state does NOT change when the pipeline is merely added to the participants list (adding ≠ selecting as main participant)
- Paperclip icon becomes inactive after the pipeline is explicitly selected as the main acting unit
- Clicking the inactive paperclip does not open any file upload dialog

**Fail:**
- Paperclip icon incorrectly becomes inactive when the pipeline is only added to participants (before selection as main unit)
- Paperclip icon remains active (false positive) after the pipeline is selected as the main acting participant with Allow Attachments OFF
- Paperclip icon incorrectly allows file uploads despite the pipeline having attachments disabled
