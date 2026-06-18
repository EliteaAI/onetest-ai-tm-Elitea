---
id: ELITEA-0898
title: "Disabling Allow Attachments Changes Paperclip to Inactive State — Toolkit Stays in List"
priority: high
type: functional
module: pipeline-attachments
status: draft
execution_type: manual
tags: [feat:attachments, feat:artifacts, feat:pipelines, nfr:usability, eng:frontend, feature:4766, eng:backend, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4766]
---
# ELITEA-0898: Disabling Allow Attachments Changes Paperclip to Inactive State — Toolkit Stays in List

**Module:** Pipeline Attachments · **Priority:** High · **Type:** Functional

**Objective:** Verify that disabling the Allow Attachments toggle changes the paperclip to inactive/disabled state in the pipeline test chat panel while the Artifact Toolkit remains in the Toolkits section.

**Coverage:**
- Allow Attachments toggled OFF and saved
- Paperclip button changes to disabled/inactive state in test chat
- Artifact Toolkit remains visible in Toolkits section

## Preconditions

- Logged in — Private project, Editor/Admin role
- Pipeline with Allow Attachments ON and Artifact Toolkit linked

## Test Data

- Pipeline: any pipeline with attachments currently enabled

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a pipeline with Allow Attachments enabled. Confirm paperclip is active in test chat. | Paperclip icon is enabled in test chat panel. |
| 2 | In the Advanced section, disable the Allow Attachments toggle. | Toggle switches to OFF. |
| 3 | Click Save. | Success notification appears. |
| 4 | Observe the test chat panel input toolbar. | Paperclip icon is now disabled/inactive (grayed out) — not removed. |
| 5 | Scroll to the Toolkits section. | Artifact Toolkit is still listed in the Toolkits section. |

## Expected Final State

Artifact Toolkit is still listed in the Toolkits section.

## Pass/Fail Criteria

**Pass:**
- Paperclip changes to inactive/disabled state after toggle OFF
- Artifact Toolkit remains in Toolkits list

**Fail:**
- Paperclip removed entirely from toolbar
- Artifact Toolkit auto-deleted from Toolkits list
