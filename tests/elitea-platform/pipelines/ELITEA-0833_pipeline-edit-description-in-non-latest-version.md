---
id: ELITEA-0833
title: "Pipeline — Edit Description in non-latest version"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, pipelines, R-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3076]
---
# ELITEA-0833: Pipeline — Edit Description in non-latest version

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Ensure that after the fix, the Description field on a non-latest Pipeline version can be edited, saved, and the change is reflected in all versions of the Pipeline.

## Preconditions

- Logged in to the application.
- User has permissions to create, update, and version Pipelines.
- No concurrent editors on the same Pipeline/version.

## Test Data

- Pipeline page: {{base_url}}
- Version name: "v2-qa-desc-20260305"
- Description to set: "Updated pipeline description for v2 - QA verification 20260305"

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Pipeline page (HelloPipeline). | Pipeline detail page loads successfully. |
| 2 | Save the Pipeline as a new version v2-qa-desc-20260305 and open it. | Version v2-qa-desc-20260305 is created and opens correctly. |
| 3 | Edit the Description field to "Updated pipeline description v2" and click Save. | UI shows a success message; Save button reflects saved state. |
| 4 | Reload or reopen the same non-latest version. | Edited Description persists in this version. |
| 5 | Open other versions (including latest/base version). | Description is updated across all versions of the Pipeline. |

## Expected Final State

Description is updated across all versions of the Pipeline.

## Pass/Fail Criteria

Pass: Description persists in the edited version and is reflected in all versions; UI shows success.

Fail: Description does not persist in the edited version or change is not propagated to other versions.
