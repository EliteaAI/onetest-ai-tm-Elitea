---
id: ELITEA-0904
title: "Multiple Files Attached in One Message — All Stored in attachments Bucket"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0904: Multiple Files Attached in One Message — All Stored in attachments Bucket

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that multiple files can be attached in a single pipeline chat message and all are stored in the attachments bucket.

**Coverage:**
- Multiple files selected in one attachment action
- All files appear as thumbnails/chips in the input
- All files stored in attachments bucket after send

## Preconditions

- Logged in — Private project
- Pipeline with Allow Attachments enabled

## Test Data

- Files: img1.png, img2.png, doc.pdf (3 files simultaneously)
- Prompt: "Analyze all attached files."

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline test chat. Click the paperclip icon. | File browser opens. |
| 2 | Select img1.png, img2.png, and doc.pdf simultaneously. | All three files appear as thumbnails/chips in the input area. |
| 3 | Type 'Analyze all attached files.' and click Send. | Message sent. Pipeline run starts. |
| 4 | Wait for pipeline run to complete. | Pipeline returns a response without errors. |
| 5 | Navigate to Artifacts → attachments bucket. | All three files appear in the bucket. |

## Expected Final State

All three files appear in the bucket.

## Pass/Fail Criteria

**Pass:**
- All 3 files accepted and shown in input
- All 3 files stored in attachments bucket
- Pipeline run completes without errors

**Fail:**
- Only some files accepted
- Files missing from bucket after send
