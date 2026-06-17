---
id: ELITEA-0910
title: "Manually Add Artifact Toolkit to Pipeline — Paperclip Becomes Active When Allow Attachments Enabled"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0910: Manually Add Artifact Toolkit to Pipeline — Paperclip Becomes Active When Allow Attachments Enabled

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that manually adding an Artifact Toolkit to a Pipeline's Toolkits section and enabling Allow Attachments activates the paperclip button in the pipeline test chat panel.

**Coverage:**
- Artifact Toolkit added via +Toolkit button
- Allow Attachments toggle enabled and saved
- Paperclip icon present and active in test chat panel after save

## Preconditions

- Logged in — Private project, Editor/Admin role
- Existing saved pipeline with no Artifact Toolkit yet
- At least one Artifact Toolkit available in the project

## Test Data

- Pipeline: "test_pipeline" 
- Artifact Toolkit: "Artifact"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the saved pipeline. | Pipeline configuration panel is displayed. |
| 2 | In the Toolkits section, click +Toolkit. | Toolkit selection dropdown opens. |
| 3 | Select 'Artifact' from the dropdown. | Toolkit is added to the pipeline's Toolkits list. |
| 4 | Go to the Advanced section, enable the Allow Attachments toggle. | Toggle switches to ON. |
| 5 | Click Save. | Success notification appears. Pipeline is saved. |
| 6 | Observe the right-side test chat panel input toolbar. | Paperclip (Attach files) icon is present and in active (enabled) state. |

## Expected Final State

Paperclip (Attach files) icon is present and in active (enabled) state.

## Pass/Fail Criteria

**Pass:**
- Artifact Toolkit appears in Toolkits list
- Allow Attachments toggle saves as ON
- Paperclip icon is visible and enabled in test chat panel

**Fail:**
- Toolkit not saved to the list
- Paperclip not visible or shown as disabled after save
