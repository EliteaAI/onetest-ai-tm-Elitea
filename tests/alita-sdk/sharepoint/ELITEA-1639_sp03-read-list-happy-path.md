---
id: ELITEA-1639
title: "SP03 - Read List (Happy Path)"
priority: critical
type: functional
module: sharepoint
status: ready
execution_type: automated
tags: [sharepoint, read_list, lists, smoke]
requirements: []
---
# ELITEA-1639: SP03 - Read List (Happy Path)

**Module:** Sharepoint · **Priority:** Critical · **Type:** Functional

**Objective:** Self-contained test that creates a test item then validates the read_list tool retrieves list items with proper fields, respecting the limit parameter.

## Preconditions

SharePoint toolkit is configured and authenticated
SHAREPOINT_TOOLKIT_NAME and SHAREPOINT_TOOLKIT_ID env vars are set
TEST_LIST_NAME env var is set to an existing SharePoint list
Valid credentials with read and write access to the list

## Test Data

SHAREPOINT_TOOLKIT_NAME: name of configured SharePoint toolkit
SHAREPOINT_TOOLKIT_ID: ID of the toolkit configuration
TEST_LIST_NAME: name of the target SharePoint list
Item fields: {Title: SP03 Test Item - {TIMESTAMP}}
Limit: 100

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Configure the SharePoint toolkit using SHAREPOINT_TOOLKIT_NAME and valid credentials | Toolkit initializes without error |
| 2 | Invoke create_list_item with TEST_LIST_NAME and Title field to create a test item | Test item created successfully with a valid item id |
| 3 | Invoke read_list with TEST_LIST_NAME and limit=100 | Tool accepts parameters and returns list items |
| 4 | Capture the response and verify items are returned | Response contains array of item objects each with properties/fields |
| 5 | Validate LLM confirms no error indicators and the created item is present in results | LLM confirms successful retrieval with the test item visible |

## Expected Final State

LLM confirms successful retrieval with the test item visible

## Pass/Fail Criteria

Test item created without error
read_list returns at least one item
Each item contains field properties
No error indicators in response
Limit parameter respected (≤100 items returned)
