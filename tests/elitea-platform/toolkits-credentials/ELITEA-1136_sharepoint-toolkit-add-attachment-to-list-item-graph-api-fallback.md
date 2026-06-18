---
id: ELITEA-1136
title: "SharePoint Toolkit - add_attachment_to_list_item Graph API Fallback"
priority: medium
type: functional
module: toolkits-credentials
status: draft
execution_type: manual
tags: [sharepoint, rest-api, backend]
requirements: []
---
# ELITEA-1136: SharePoint Toolkit - add_attachment_to_list_item Graph API Fallback

**Module:** Toolkits Credentials · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that SharePoint toolkit's `add_attachment_to_list_item` tool correctly falls back to Microsoft Graph API when SharePoint REST API v1 is unavailable or fails.

## Preconditions

- User logged in to Elitea stage environment
- SharePoint credentials configured with Microsoft Graph API access
- Test SharePoint site and list available
- Test file prepared for attachment upload

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a SharePoint list item via API | List item created successfully, item_id returned |
| 2 | Configure SharePoint credentials to simulate REST API v1 failure (block REST endpoint or use Graph-only auth) | Environment configured for REST API failure scenario |
| 3 | Use `add_attachment_to_list_item` tool with: list_id, item_id, file_name='test_attachment.txt', file_content='Test content' | Tool attempts REST API first, fails, falls back to Graph API, succeeds |
| 4 | Check list item via Graph API for attachment | Attachment present on list item |
| 5 | Create another SharePoint list item | List item created successfully |
| 6 | Configure environment with Graph API only (no REST API access) | Environment configured for Graph API only |
| 7 | Use `add_attachment_to_list_item` tool | Tool uses Graph API endpoint `/sites/{site-id}/lists/{list-id}/items/{item-id}/attachments` directly, succeeds |
| 8 | Create a third list item | List item created successfully |
| 9 | Configure SharePoint credentials with REST API v1 access | Environment configured for REST API access |
| 10 | Use `add_attachment_to_list_item` tool | Tool uses REST API successfully (no fallback needed, baseline check) |

## Expected Final State

Tool uses REST API successfully (no fallback needed, baseline check)

## Pass/Fail Criteria

PASS: All three test cases succeed - REST fallback works, Graph API direct works, REST baseline works
FAIL: Test Case 1 or 2 fails with hard error (no fallback occurs)
