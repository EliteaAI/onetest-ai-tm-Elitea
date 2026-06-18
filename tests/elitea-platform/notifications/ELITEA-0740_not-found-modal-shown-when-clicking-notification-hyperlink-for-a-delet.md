---
id: ELITEA-0740
title: "\"Not Found\" modal shown when clicking notification hyperlink for a deleted index"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, r-2.0.3, indexes]
requirements: [EliteaAI/elitea_issues#4698]
---
# ELITEA-0740: "Not Found" modal shown when clicking notification hyperlink for a deleted index

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a user clicks a notification hyperlink pointing to an index that has since been deleted, a user-friendly "not found" modal is displayed instead of a blank/empty page.

**Coverage:**
- Notification Center hyperlink behavior for deleted resources
- Error state UI (not found modal)
- No blank page / silent failure

**Linked to:** Enhancement EliteaAI/elitea_issues#4698, Milestone R-2.0.3

## Preconditions

1. User is logged in to ELITEA.
2. An Indexing Toolkit with at least one index exists in the project.
3. An indexing operation (success or failure) was triggered, generating a notification with a hyperlink to that index (visible via the bell icon in the top navigation).
4. The index has since been deleted from the Toolkit.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the bell icon in the top navigation to open the Notification Center. | Notification Center dropdown opens and displays the list of notifications. |
| 2 | Locate a notification referencing the now-deleted index (hyperlink on the index name). | Notification is visible in the list with a clickable hyperlink. |
| 3 | Click the hyperlink pointing to the deleted index. | A user-friendly 'not found' modal/dialog is displayed (e.g., 'Index not found.' or 'This resource no longer exists.'). The page does NOT render blank or empty. The modal is dismissible (has a close/OK button). No JS crash or unhandled error occurs. |
| 4 | Dismiss the modal (click Close/OK). | Modal closes. The user can continue navigating normally within the application. |

## Expected Final State

Modal closes. The user can continue navigating normally within the application.

## Pass/Fail Criteria

- 'Not found' modal appears immediately after clicking the hyperlink
- Modal contains a clear, readable message about the resource being unavailable
- Modal has a working dismiss control (Close/OK)
- Page is not blank/empty after clicking the link
- No unhandled JS error or crash occurs
