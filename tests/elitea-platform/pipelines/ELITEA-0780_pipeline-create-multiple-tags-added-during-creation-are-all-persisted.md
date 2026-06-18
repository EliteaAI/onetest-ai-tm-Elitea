---
id: ELITEA-0780
title: "[Pipeline Create] Multiple Tags Added During Creation Are All Persisted — Direct + Chat Participant [Parametrized]"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [bug-env:next, feat:tags, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5151]
---
# ELITEA-0780: [Pipeline Create] Multiple Tags Added During Creation Are All Persisted — Direct + Chat Participant [Parametrized]

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that adding multiple tags (system-existing and system-new) during pipeline creation correctly persists all of them after save, across both creation entry points.

**Coverage:**
- Creating pipeline via the direct Pipelines page creation form
- Creating pipeline via Chat Participants flow
- System-existing tags (already used elsewhere in the system) are persisted
- System-new tags (never used anywhere in the system) are persisted
- All tags survive navigation away and page reload

## Preconditions

- Logged in to ELITEA (next.elitea.ai)
- Permissions to create pipelines
- Identify a tag already in use by at least one other agent or pipeline in the system (system-existing tag)
- Prepare 2 tag values that have never been used anywhere in the system (system-new tags)
- Browser: Chrome latest

## Test Data

**Variant A — Direct creation:**
- Pipeline name: TagTestPipeline_Create
- Pipeline description: Test pipeline to verify tag persistence on creation
- Tags: ExistingSystemTag (system-existing), BrandNewPipeTag_Create1 (system-new), BrandNewPipeTag_Create2 (system-new)

**Variant B — Chat Participant creation:**
- Pipeline name: TagTestPipeline_ChatParticipant
- Pipeline description: Test pipeline created via Chat Participants to verify tag persistence
- Tags: ExistingSystemTag (system-existing), BrandNewPipeTag_Chat1 (system-new), BrandNewPipeTag_Chat2 (system-new)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | **[Variant A]** Navigate to Pipelines → click Create Pipeline. **[Variant B]** Navigate to Chat, open the Participants panel, and initiate Create Pipeline from the Chat Participants flow. | Pipeline creation form/modal opens. |
| 2 | Fill in the pipeline name and description as per the test data for the chosen variant. | Name and description fields are populated. |
| 3 | Add the system-existing tag (ExistingSystemTag) to the tag field. | Tag chip appears in the field. |
| 4 | Add the first system-new tag. | Second chip appears; 2 chips visible. |
| 5 | Add the second system-new tag. | Third chip appears; 3 chips visible. |
| 6 | Click Save / Create. | Pipeline is created successfully with no error. |
| 7 | Navigate to the Pipelines list and open the newly created pipeline. | Pipeline detail view loads. |
| 8 | Inspect the tag field. | All 3 tags — system-existing and both system-new — are present. |

## Expected Final State

All 3 tags — system-existing and both system-new — are present.

## Pass/Fail Criteria

**Pass:**
- All 3 tags visible after creation and navigation back to the pipeline
- Both variant A and variant B produce the correct result

**Fail:**
- Any tag missing after opening the created pipeline
- Regression in either creation flow
