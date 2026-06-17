---
id: ELITEA-0908
title: "Paperclip is Inactive in Pipeline Test Chat When Attachments Not Enabled"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0908: Paperclip is Inactive in Pipeline Test Chat When Attachments Not Enabled

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that the paperclip button does not appear active in a pipeline's test chat panel when Allow Attachments is not enabled.

**Coverage:**
- Pipeline with Allow Attachments OFF (no Artifact Toolkit configured)
- Test chat panel contains only: text input, model selector, Send button
- No active paperclip / attach files control present

## Preconditions

- Logged in — Private project
- Existing pipeline with Allow Attachments disabled (no Artifact Toolkit configured)

## Test Data

- Pipeline: any pipeline without attachments configured

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a saved pipeline that has Allow Attachments set to OFF. | Pipeline opens. Advanced section shows toggle OFF. |
| 2 | Inspect the right-side test chat panel input toolbar. | Toolbar shows: text input, model selector, Send button and inactive paperclin icon. |
| 3 | Confirm that the paperclip button in the toolbar is inactive. | Paperclip button in the toolbar is inactive. |

## Expected Final State

Paperclip button in the toolbar is inactive.

## Pass/Fail Criteria

**Pass:**
- No active paperclip button in test chat panel

**Fail:**
- Paperclip button is activewhen attachments not configured
