---
id: ELITEA-0894
title: "Pipeline as Chat Participant — Attached File Processed and Stored in attachments Bucket"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0894: Pipeline as Chat Participant — Attached File Processed and Stored in attachments Bucket

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify the full end-to-end flow when using a pipeline with attachments enabled as a Chat participant — file is attached via the paperclip, pipeline run completes, the response references file content, and the file is stored in the `attachments` bucket.

**Coverage:**
- Pipeline with attachments added as Chat participant
- File attached and sent in a Chat conversation via the paperclip icon
- Pipeline run completes and response references the content of the attached file
- Attached file stored in `attachments` Artifact bucket after send

## Preconditions

- Logged in — Private project
- Pipeline with Allow Attachments enabled (Artifact Toolkit linked, LLM-capable)
- Pipeline added as a participant in an open Chat conversation
- Paperclip icon active in the Chat input toolbar

## Test Data

- File: sample.pdf (contains identifiable content)
- Prompt: "What is the main topic of this document?"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat. Open a conversation with the pipeline added as a participant. Confirm the paperclip icon is active in the chat input toolbar. | Chat input shows active paperclip. Pipeline shown as participant at the bottom of the chat input. |
| 2 | Click the paperclip and select sample.pdf. | File thumbnail appears in the chat input. |
| 3 | Type 'What is the main topic of this document?' and click Send. | Message sent. Pipeline run starts. |
| 4 | Wait for the pipeline run to complete. | Pipeline returns a response in the chat. |
| 5 | Inspect the response content. | Response references the content of sample.pdf (e.g., mentions the document topic or acts on the file content). |
| 6 | Navigate to Artifacts → attachments bucket. | sample.pdf is present in the bucket with correct name and non-zero size. |

## Expected Final State

sample.pdf is present in the bucket with correct name and non-zero size.

## Pass/Fail Criteria

**Pass:**
- Pipeline run completes without errors
- Response references content from the attached file
- File present in attachments bucket with correct name and non-zero size

**Fail:**
- Pipeline run errors when file is attached via Chat
- Response does not reference file content
- File missing from attachments bucket
