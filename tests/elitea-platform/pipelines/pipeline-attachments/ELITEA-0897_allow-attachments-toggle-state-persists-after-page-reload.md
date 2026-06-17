---
id: ELITEA-0897
title: "Allow Attachments Toggle State Persists After Page Reload"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0897: Allow Attachments Toggle State Persists After Page Reload

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that the Allow Attachments toggle state and linked Artifact Toolkit survive a full browser page reload.

**Coverage:**
- Toggle remains ON after reload
- Artifact Toolkit still shows paperclip indicator after reload
- Paperclip active in test chat after reload

## Preconditions

- Logged in — Private project, Editor/Admin role
- Existing saved pipeline with Allow Attachments currently OFF and an Artifact Toolkit in its toolkit list

## Test Data

- Pipeline: any pipeline with Allow Attachments ON

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the saved pipeline. Expand the Advanced section. | Allow Attachments toggle is present and set to OFF. |
| 2 | Enable the Allow Attachments toggle. | Toggle switches to ON. |
| 3 | Click Save. | Success notification appears. Pipeline is saved. |
| 4 | Press Shift+F5 to fully reload the page. | Page reloads. |
| 5 | Navigate back to the same pipeline and expand the Advanced section. | Allow Attachments toggle is still ON — the saved state persisted after reload. |
| 6 | Observe the test chat panel input toolbar. | Paperclip icon is still active/enabled. |

## Expected Final State

Paperclip icon is still active/enabled.

## Pass/Fail Criteria

**Pass:**
- Toggle ON state persists after reload
- Artifact Toolkit paperclip indicator persists
- Paperclip active in test chat after reload

**Fail:**
- Toggle reverts to OFF after reload
- Toolkit loses paperclip indicator after reload
