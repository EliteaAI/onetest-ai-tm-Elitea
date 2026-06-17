---
id: ELITEA-0665
title: "Exported ZIP file for Pipeline with nested entities uses the Pipeline name as filename"
priority: medium
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:pipelines, R-2.0.1, eng:ui]
requirements: [ProjectAlita/projectalita.github.io#3725]
---
# ELITEA-0665: Exported ZIP file for Pipeline with nested entities uses the Pipeline name as filename

**Module:** Export Import · **Priority:** Medium · **Type:** Functional

**Objective:** Objective:
Verify that exporting a Pipeline containing nested entities produces a ZIP file named after the Pipeline so users can easily identify exported pipelines.

Coverage:
- Export a Pipeline that contains nested entities (tasks, sub-pipelines, or referenced agents)
- Confirm that a ZIP file is downloaded when Export is invoked
- Confirm the downloaded ZIP filename matches the Pipeline name with the `.zip` extension

## Preconditions

- User is logged in to the application.
- User has permission to view Pipelines and export Pipelines.
- A Pipeline named `test-pipeline-export` is created and contains at least one nested entity.
- User has access to the browser Downloads folder.

## Test Data

Pipeline name: `test-pipeline-export`
Expected filename: `test-pipeline-export.zip`

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Pipelines page. | Pipelines list loads and displays test-pipeline-export. |
| 2 | Open the Pipeline named test-pipeline-export. | Pipeline editor opens for test-pipeline-export. |
| 3 | Click the Export button in the Pipeline editor and confirm export if a modal appears. | Export process starts and a ZIP file is downloaded. |
| 4 | Inspect the downloaded file name in the Downloads folder. | The downloaded file name is test-pipeline-export.zip. |

## Expected Final State

The downloaded file name is test-pipeline-export.zip.

## Pass/Fail Criteria

Pass:
- A ZIP file is downloaded successfully.
- The downloaded ZIP filename matches `test-pipeline-export.zip`.

Fail:
- No ZIP file is downloaded.
- The downloaded ZIP filename does not match `test-pipeline-export.zip`.
