---
id: ELITEA-0892
title: "Paperclip Icon Activates Immediately After Enabling Allow Attachments on Pipeline Participant — New Chat"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:pipelines, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5030]
---
# ELITEA-0892: Paperclip Icon Activates Immediately After Enabling Allow Attachments on Pipeline Participant — New Chat

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that the paperclip icon activates immediately in the chat message input area when the Allow Attachments toggle is enabled on a pipeline participant — without requiring a page refresh.

**Coverage:**
- New chat session with a pipeline participant that has Allow Attachments OFF
- Enable the Allow Attachments toggle via the pipeline settings panel within the chat
- Save the pipeline settings
- Paperclip icon updates to active state in real time (no page refresh needed)
- Paperclip icon remains active on subsequent page load as well

## Preconditions

- Logged in to {{base_url}}
- A pipeline exists with Allow Attachments toggle set to OFF (no Artifact Toolkit configured)
- The pipeline has at least one published version available
- A fresh/new chat session is available

## Test Data

- Pipeline: any pipeline with Allow Attachments OFF (e.g., name "Attachments pipeline")
- Environment: {{base_url}}
- Browser: Chrome latest

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a new chat conversation (no prior messages) | Empty chat session opens; the message input area is visible |
| 2 | Add the pipeline (with Allow Attachments OFF) as a participant via the Participants panel | Pipeline is listed in the Participants section; the paperclip icon in the message input area is inactive (greyed out / not clickable) |
| 3 | In the Participants panel, hover over the pipeline and click the Edit (pencil) icon to open its settings in the Canvas editor | Pipeline Canvas editor opens showing the current configuration |
| 4 | Navigate to the Configuration tab → ADVANCED section and click the Allow Attachments toggle to enable it; configure an Artifact Toolkit (select existing or create new) when prompted, then click Save | Allow Attachments toggle turns ON; Canvas editor closes or shows saved state |
| 5 | Observe the paperclip icon in the chat message input area immediately after saving (without refreshing the page) | Paperclip icon becomes active (highlighted / clickable) immediately — no page refresh is needed. Pipeline is added as the main acting participant (substituting chat's default LLM model) |
| 6 | Click the paperclip icon | File attachment options appear (Attach files / Attachment settings), confirming the icon is functional |

## Expected Final State

File attachment options appear (Attach files / Attachment settings), confirming the icon is functional

## Pass/Fail Criteria

**Pass:**
- Paperclip icon transitions from inactive to active state immediately after saving the Allow Attachments toggle ON
- No page refresh is required for the icon state to update
- Clicking the active paperclip icon opens the attachment options

**Fail:**
- Paperclip icon remains inactive after saving the toggle ON (page refresh still required)
- Paperclip icon state does not change at all after saving
- Page refresh is required to observe the correct icon state
