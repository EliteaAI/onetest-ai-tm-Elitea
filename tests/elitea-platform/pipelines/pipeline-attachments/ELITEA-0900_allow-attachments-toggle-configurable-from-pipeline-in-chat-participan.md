---
id: ELITEA-0900
title: "Allow Attachments Toggle Configurable From Pipeline in Chat Participant Panel"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0900: Allow Attachments Toggle Configurable From Pipeline in Chat Participant Panel

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a pipeline is added as a Chat participant and its configuration is opened from the Chat participants panel, the Allow Attachments toggle is present and can be configured.

**Coverage:**
- Pipeline config accessible from Chat \u2192 Participants panel
- Allow Attachments toggle visible in Advanced section from Chat context
- Changes saved from Chat participant panel apply correctly

## Preconditions

- Logged in — Private project, Editor/Admin role
- A pipeline exists with Allow Attachments currently OFF
- Artifact Toolkit added to pipeline's toolkit list

## Test Data

- Pipeline: any saved pipeline with an Artifact Toolkit in its toolkit list but Allow Attachments OFF

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Open a conversation. In the Participants panel, click Add pipeline and add the target pipeline. | Pipeline is added as participant. |
| 2 | Click the pipeline name or its edit/config icon in the participants panel. | Pipeline configuration panel opens from the Chat context. |
| 3 | Expand the Advanced section. | Allow Attachments toggle is present. |
| 4 | Enable the Allow Attachments toggle. Click Save. | Success notification appears. |
| 5 | Confirm paperclip icon in the Chat input becomes active. | Paperclip is enabled in the chat input toolbar. |

## Expected Final State

Paperclip is enabled in the chat input toolbar.

## Pass/Fail Criteria

**Pass:**
- Allow Attachments toggle accessible from Chat participant panel
- Toggle change saves correctly
- Paperclip becomes active in Chat input after enabling

**Fail:**
- Pipeline config from Chat participant panel does not show the toggle
- Changes do not persist after save from Chat context
