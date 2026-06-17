---
id: ELITEA-0911
title: "Attached File Stored in attachments Artifact Bucket"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0911: Attached File Stored in attachments Artifact Bucket

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that a file attached via the pipeline test chat is stored in the attachments Artifact bucket with correct metadata.

**Coverage:**
- File appears in attachments bucket after pipeline chat send
- File metadata (name, size) is correct
- No file stored in an unrelated bucket

## Preconditions

- Logged in — Private project
- Pipeline with Allow Attachments enabled
- attachments Artifact bucket exists

## Test Data

- File: sample.pdf
- Expected bucket: attachments

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline test chat. Attach sample.pdf via the paperclip icon. | File is selected; thumbnail/filename shown in input. |
| 2 | Type a prompt ('Summarize this.') and click Send. | Pipeline run executes. |
| 3 | Navigate to Artifacts from the sidebar. | Artifacts section opens. |
| 4 | Open the attachments bucket. | Bucket file list is displayed. |
| 5 | Locate sample.pdf in the file list. | File is present with correct name and non-zero size. |

## Expected Final State

File is present with correct name and non-zero size.

## Pass/Fail Criteria

**Pass:**
- sample.pdf present in attachments bucket with correct name and size

**Fail:**
- File absent from attachments bucket
- File stored in wrong bucket
