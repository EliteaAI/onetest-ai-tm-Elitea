---
id: ELITEA-0909
title: "Pipeline as Chat Participant: Paperclip Works and File Is Sent"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0909: Pipeline as Chat Participant: Paperclip Works and File Is Sent

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a pipeline with attachments enabled is added as a participant in a Chat conversation, the file attachment button is active and a file can be attached and sent.

**Coverage:**
- Pipeline with attachments added as Chat participant
- Paperclip icon active in Chat input toolbar
- File attached and message sent without errors
- Pipeline run completes

## Preconditions

- Logged in — Private project
- Pipeline with Allow Attachments enabled (Artifact Toolkit linked)
- Chat conversation available

## Test Data

- Pipeline: any pipeline with Allow Attachments ON
- File: image.png
- Prompt: "What is in this image?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat and open a conversation. | Chat conversation is open. |
| 2 | In the Participants panel, click Add pipeline and select the pipeline with attachments enabled. | Pipeline is added as a participant. |
| 3 | Observe the chat input toolbar. | Paperclip (Attach files) button is active. |
| 4 | Click the paperclip and select image.png. | File thumbnail appears in the input. |
| 5 | Type 'What is in this image?' and click Send. | Message sent; pipeline run starts. |
| 6 | Wait for the run to complete. | Pipeline returns a response in the chat without errors. |

## Expected Final State

Pipeline returns a response in the chat without errors.

## Pass/Fail Criteria

**Pass:**
- Paperclip active after pipeline with attachments is added as participant
- File sent and pipeline run completes without errors

**Fail:**
- Paperclip inactive or absent
- Pipeline run errors on file-attached message
