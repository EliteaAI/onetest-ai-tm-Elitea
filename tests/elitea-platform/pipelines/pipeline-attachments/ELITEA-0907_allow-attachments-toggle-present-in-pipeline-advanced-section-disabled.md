---
id: ELITEA-0907
title: "Allow Attachments Toggle Present in Pipeline Advanced Section — Disabled by Default"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0907: Allow Attachments Toggle Present in Pipeline Advanced Section — Disabled by Default

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Allow Attachments toggle is present in the Advanced section of a saved Pipeline configuration, disabled by default, and absent on an unsaved pipeline.

**Coverage:**
- Toggle present in Advanced section of an existing saved pipeline
- Toggle default state is OFF
- Toggle absent before pipeline is saved for the first time

## Preconditions

- Logged in to {{base_url}} — Private project
- At least one existing saved pipeline available
- Editor or Admin role

## Test Data

- Existing pipeline: any saved pipeline (e.g., "regression tes")
- New pipeline: unsaved (Name + Description filled, not yet saved)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines from the sidebar. | Pipelines list page is displayed. |
| 2 | Click on an existing saved pipeline. | Pipeline configuration panel opens on the left. |
| 3 | Expand the Advanced section in the left configuration panel. | Advanced section expands showing Step limit field and Allow Attachments toggle. |
| 4 | Observe the state of the Allow Attachments toggle. | Toggle is present and set to OFF (disabled) by default. |
| 5 | Click Create in the sidebar. Fill in Name and Description fields. Do NOT click Save. | New pipeline creation form is shown; only basic fields visible. |
| 6 | Expand the Advanced section on the unsaved pipeline. | Allow Attachments toggle is NOT present / not accessible. |

## Expected Final State

Allow Attachments toggle is NOT present / not accessible.

## Pass/Fail Criteria

**Pass:**
- Toggle present and OFF in existing saved pipeline
- Toggle absent in unsaved pipeline

**Fail:**
- Toggle missing from saved pipeline
- Toggle present before first save
