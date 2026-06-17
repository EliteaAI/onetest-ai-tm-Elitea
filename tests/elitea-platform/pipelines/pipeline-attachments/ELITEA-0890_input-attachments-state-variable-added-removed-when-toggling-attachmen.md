---
id: ELITEA-0890
title: "'input_attachments' State Variable Added/Removed When Toggling Attachments in Conversation Canvas Editor [Bug EliteaAI/elitea_issues#5079]"
priority: high
type: functional
module: pipeline-attachments
status: ready
execution_type: manual
tags: [feat:attachments, feat:pipelines, eng:frontend, feat:chat, r-2.0.3]
requirements: [EliteaAI/elitea_issues#5079]
---
# ELITEA-0890: 'input_attachments' State Variable Added/Removed When Toggling Attachments in Conversation Canvas Editor [Bug EliteaAI/elitea_issues#5079]

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that the `input_attachments` state variable is automatically added to the pipeline's States list when the Attachments toggle is enabled via the conversation canvas editor, and automatically removed when the toggle is disabled.

**Bug Reference:** EliteaAI/elitea_issues#5079

## Preconditions

- Logged in to {{base_url}}
- A pipeline exists with at least one published version
- Chat page is accessible

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Chat page and create or open an existing conversation | Chat is open with the Participants section visible |
| 2 | In the PARTICIPANTS section, initiate creation of a new pipeline or open an existing pipeline in edit mode via the canvas editor | Pipeline canvas editor opens |
| 3 | Navigate to the Flow Editor tab → States section. Note the current States list (input_attachments should NOT be present) | States list is visible; input_attachments is absent |
| 4 | Enable the Attachments toggle on the Configuration tab | Toggle turns ON |
| 5 | Review the States list | input_attachments state variable appears in the States list automatically |
| 6 | Disable the Attachments toggle | Toggle turns OFF |
| 7 | Review the States list again | input_attachments state variable is removed from the States list |

## Expected Final State

input_attachments state variable is removed from the States list

## Pass/Fail Criteria

PASS: `input_attachments` state variable automatically added to States on toggle ON, and removed on toggle OFF — via conversation canvas editor
FAIL: `input_attachments` not added after enabling toggle (bug EliteaAI/elitea_issues#5079); or not removed when disabled
