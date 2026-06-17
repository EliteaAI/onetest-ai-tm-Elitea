---
id: ELITEA-0912
title: "Happy Path: Attach File via Pipeline Test Chat — Image / Document / Code [Parametrized]"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0912: Happy Path: Attach File via Pipeline Test Chat — Image / Document / Code [Parametrized]

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that attaching a file via the pipeline test chat triggers a successful pipeline run and the pipeline responds using the file content.

**Coverage:**
- Image file attached → pipeline responds with visual analysis
- Document file attached → pipeline responds referencing document content
- Code file attached → pipeline responds referencing code content
- All variations stored in the attachments Artifact bucket

## Preconditions

- Logged in — Private project, Editor/Admin role
- Pipeline with Allow Attachments enabled and an Artifact Toolkit linked (LLM-capable pipeline)
- Paperclip icon active in test chat panel

## Test Data

| # | File | Prompt |
|---|---|---|
| 1 | image.png (< 5 MB) | "Describe what you see in this image." |
| 2 | sample.pdf | "What is the main topic of this document?" |
| 3 | script.py | "Explain what this code does." |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline with Allow Attachments enabled. Confirm paperclip is active in test chat. | Pipeline configuration is loaded, paperclip is active in test chat panel. |
| 2 | In the test chat panel, click the paperclip icon. | File browser or attachment dialog opens. |
| 3 | Select the test file from the table (repeat for each row). | File thumbnail or filename appears in the input area. |
| 4 | Type the corresponding prompt from the table and click Send. | Message is sent; pipeline run starts. |
| 5 | Wait for the pipeline run to complete. | Pipeline returns a response in the chat. |
| 6 | Observe the response content. | Response references content from the attached file (visual description / document topic / code explanation). |
| 7 | Navigate to Artifacts → attachments bucket. | The uploaded file appears in the bucket file list. |

## Expected Final State

The uploaded file appears in the bucket file list.

## Pass/Fail Criteria

**Pass:**
- Pipeline run completes without errors for all three file types
- Response content reflects the attached file's content
- All three files appear in the attachments bucket

**Fail:**
- Pipeline run errors or returns a response unrelated to the file
- File not stored in attachments bucket
- Paperclip non-functional for any file type
