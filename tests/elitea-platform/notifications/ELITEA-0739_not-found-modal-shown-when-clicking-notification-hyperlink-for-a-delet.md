---
id: ELITEA-0739
title: "\"Not Found\" modal shown when clicking notification hyperlink for a deleted bucket"
priority: medium
type: functional
module: notifications
status: draft
execution_type: manual
tags: [feat:notifications, artifacts, buckets, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4698]
---
# ELITEA-0739: "Not Found" modal shown when clicking notification hyperlink for a deleted bucket

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that when a user clicks a notification hyperlink pointing to an Artifact bucket that has since been permanently deleted, a user-friendly "not found" modal is displayed instead of a blank/empty page.

**Coverage:**
- Notification Center hyperlink behavior for deleted resources (Artifacts/Buckets)
- Error state UI (not found modal)
- No blank page / silent failure

**Linked to:** Enhancement EliteaAI/elitea_issues#4698, Milestone R-2.0.3

## Preconditions

1. User is logged in to ELITEA.
2. An Artifact bucket exists in the project and a notification was generated that contains a hyperlink to that bucket (visible via the bell icon in the top navigation).
3. The bucket has since been permanently deleted from the Artifacts menu (all its files are gone and cannot be recovered).

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Click the bell icon in the top navigation to open the Notification Center. | Notification Center dropdown opens and displays the list of notifications. |
| 2 | Locate a notification containing a hyperlink to the now-deleted bucket. | Notification is visible in the list with a clickable hyperlink referencing the bucket. |
| 3 | Click the hyperlink pointing to the deleted bucket. | A user-friendly 'not found' modal/dialog is displayed (e.g., 'Bucket not found. It may have been deleted.' or 'This resource no longer exists.'). The page does NOT render blank or empty. The modal is dismissible (has a close/OK button). No JS crash or unhandled error occurs. |
| 4 | Dismiss the modal (click Close/OK). | Modal closes. The user can continue navigating normally within the application. |

## Expected Final State

Modal closes. The user can continue navigating normally within the application.

## Pass/Fail Criteria

- 'Not found' modal appears immediately after clicking the hyperlink
- Modal contains a clear, readable message about the resource being unavailable
- Modal has a working dismiss control (Close/OK)
- Page is not blank/empty after clicking the link
- No unhandled JS error or crash occurs
