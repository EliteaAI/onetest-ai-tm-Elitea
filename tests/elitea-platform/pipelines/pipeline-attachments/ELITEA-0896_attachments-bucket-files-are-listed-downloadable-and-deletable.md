---
id: ELITEA-0896
title: "Attachments Bucket Files Are Listed, Downloadable, and Deletable"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0896: Attachments Bucket Files Are Listed, Downloadable, and Deletable

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that files uploaded via pipeline attachment are visible, downloadable, and deletable from the Artifacts section.

**Coverage:**
- Files listed in attachments bucket with name and size
- Download action works for an uploaded file
- Delete action removes the file from the bucket

## Preconditions

- Logged in — Private project
- At least one file uploaded via pipeline chat attachment

## Test Data

- File: sample.pdf (previously uploaded via pipeline chat attachment)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts → attachments bucket. | Bucket file list shows sample.pdf. |
| 2 | Click the Download action on sample.pdf. | File downloads to local machine without error. |
| 3 | Click the Delete action on sample.pdf. Confirm deletion if prompted. | File is removed. sample.pdf no longer appears in the bucket file list. |

## Expected Final State

File is removed. sample.pdf no longer appears in the bucket file list.

## Pass/Fail Criteria

**Pass:**
- File listed with correct name and size
- Download completes without error
- Delete removes file from bucket list

**Fail:**
- File not listed despite successful upload
- Download fails or produces a corrupt file
- Delete errors or file reappears after deletion
