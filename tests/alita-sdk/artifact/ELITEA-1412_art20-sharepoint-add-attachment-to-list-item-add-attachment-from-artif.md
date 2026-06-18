---
id: ELITEA-1412
title: "ART20 - SharePoint add_attachment_to_list_item: Add Attachment from Artifact"
priority: critical
type: functional
module: artifact
status: ready
execution_type: automated
tags: []
requirements: []
---
# ELITEA-1412: ART20 - SharePoint add_attachment_to_list_item: Add Attachment from Artifact

**Module:** Artifact · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the SharePoint add_attachment_to_list_item tool adds an attachment from artifact storage to a SharePoint list item. Test is self-contained: creates its own list item before adding the attachment.

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
item Title: 'ART18 Test Item for Attachment - {timestamp}'
filepath: SHAREPOINT_TEST_ARTIFACT_ID (env var)
filename: 'ART18_test_attachment.txt'
replace: true
item_id: dynamically extracted from create_list_item result

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure SharePoint and Artifact toolkits | Both toolkits initialized successfully |
| 2 | Call `create_list_item` tool with list_title=SHAREPOINT_TEST_LIST and fields={Title: 'ART18 Test Item for Attachment - {timestamp}'} | List item is created and returned with a valid numeric id |
| 3 | Extract item_id from the created_item response (dict.get('id') or regex from JSON string) | item_id is extracted as a string |
| 4 | Call `add_attachment_to_list_item` with list_title, item_id, filepath=SHAREPOINT_TEST_ARTIFACT_ID, filename='ART18_test_attachment.txt', replace=true | Attachment is added without error |
| 5 | LLM validator checks: item_created=true (has valid id), attachment_added=true, result contains id/name/size, name matches filename, size > 0 | test_results: {test_passed: true, item_created: true, attachment_added: true, has_attachment_id: true, name_matches_filename: true, size_positive: true} |

## Expected Final State

test_results: {test_passed: true, item_created: true, attachment_added: true, has_attachment_id: true, name_matches_filename: true, size_positive: true}

## Pass/Fail Criteria

test_passed = true
item_created = true
attachment_added = true
has_attachment_id = true
name_matches_filename = true
size_positive = true
no_errors = true
