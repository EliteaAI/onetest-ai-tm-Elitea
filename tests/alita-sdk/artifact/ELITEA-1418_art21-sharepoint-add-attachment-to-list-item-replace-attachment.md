---
id: ELITEA-1418
title: "ART21 - SharePoint add_attachment_to_list_item: Replace Attachment"
priority: high
type: functional
module: artifact
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1418: ART21 - SharePoint add_attachment_to_list_item: Replace Attachment

**Module:** Artifact · **Priority:** High · **Type:** Functional

**Objective:** Verify the SharePoint add_attachment_to_list_item tool replaces an existing attachment when replace=True. Self-contained: creates list item then adds the same artifact attachment twice.

Preconditions:
- SharePoint toolkit is configured with valid credentials
- Artifact toolkit is configured with valid credentials
- SHAREPOINT_TEST_LIST exists
- SHAREPOINT_TEST_ARTIFACT_ID points to a valid artifact file

## Preconditions

SharePoint toolkit is configured with SHAREPOINT_TOOLKIT_ID and SHAREPOINT_TOOLKIT_NAME.
Artifact toolkit is configured with ARTIFACT_TOOLKIT_ID and ARTIFACT_TOOLKIT_NAME.
SHAREPOINT_TEST_LIST exists.
SHAREPOINT_TEST_ARTIFACT_ID is set to a valid artifact file ID.

## Test Data

list_title: SHAREPOINT_TEST_LIST (env var)
item Title: 'ART19 Test Item for Replace Attachment - {timestamp}'
filepath: SHAREPOINT_TEST_ARTIFACT_ID (env var)
filename: 'ART19_test_attachment.txt'
replace: true
item_id: dynamically extracted from create_list_item result
Both attachment calls use identical parameters

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure SharePoint and Artifact toolkits | Both toolkits initialized successfully |
| 2 | Call `create_list_item` tool with list_title=SHAREPOINT_TEST_LIST and fields={Title: 'ART19 Test Item for Replace Attachment - {timestamp}'} | List item is created with a valid numeric id |
| 3 | Extract item_id from the created_item response | item_id is extracted as a string |
| 4 | Call `add_attachment_to_list_item` (first time) with list_title, item_id, filepath=SHAREPOINT_TEST_ARTIFACT_ID, filename='ART19_test_attachment.txt', replace=true | First attachment is added successfully with id, name, size metadata |
| 5 | Call `add_attachment_to_list_item` (second time) with identical parameters — same item_id, filename, and replace=true | Second attachment replaces the first without error |
| 6 | LLM validator checks: item_created=true, both operations succeeded, both results contain id/name/size, same filename confirms replacement, no errors | test_results: {test_passed: true, item_created: true, first_attachment_succeeded: true, second_attachment_succeeded: true, both_have_metadata: true} |

## Expected Final State

test_results: {test_passed: true, item_created: true, first_attachment_succeeded: true, second_attachment_succeeded: true, both_have_metadata: true}

## Pass/Fail Criteria

test_passed = true
item_created = true
first_attachment_succeeded = true
second_attachment_succeeded = true (replacement)
both_have_metadata = true
no_errors = true
