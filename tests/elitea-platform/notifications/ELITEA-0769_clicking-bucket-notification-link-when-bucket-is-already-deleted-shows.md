---
id: ELITEA-0769
title: "Clicking Bucket Notification Link When Bucket Is Already Deleted Shows Graceful Fallback (No Crash)"
priority: medium
type: functional
module: notifications
status: ready
execution_type: manual
tags: [feat:notifications, user_story:3414, feat:artifacts, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#4043]
---
# ELITEA-0769: Clicking Bucket Notification Link When Bucket Is Already Deleted Shows Graceful Fallback (No Crash)

**Module:** Notifications · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that clicking the bucket name hyperlink in an expiration notification when the referenced bucket has already been deleted does not crash the application — a graceful fallback or error message is shown instead.

**Coverage:**
- Notification link clicked after the target bucket has been deleted
- No application crash or unhandled JavaScript error occurs
- Graceful fallback shown (e.g., "Bucket not found" message, redirect to Artifacts root, or empty state)
- Application and notification panel remain functional after the failed navigation

## Preconditions

- Logged in as a project member with Artifacts create/delete permissions
- Environment: {{base_url}}
- Browser: Chrome (latest)

## Test Data

- Bucket name: `deleted-bucket-nav-test`
- Retention: Days = 1 (triggers immediate notification on creation per edge case rule)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts from the sidebar. Create a new bucket named `deleted-bucket-nav-test` with Days = 1 retention. | Bucket is created. Notification fires immediately and appears in the notification panel referencing `deleted-bucket-nav-test`. |
| 2 | Open the notification panel. Confirm the expiration notification for `deleted-bucket-nav-test` is visible with its bucket name as a hyperlink. | Notification is present with a clickable `deleted-bucket-nav-test` link. |
| 3 | Navigate to Artifacts. Select `deleted-bucket-nav-test` and delete it. | Bucket is deleted. `deleted-bucket-nav-test` no longer appears in the Artifacts sidebar. |
| 4 | Open the notification panel. Locate the expiration notification for `deleted-bucket-nav-test`. | The notification still appears in the panel (it was not removed when the bucket was deleted). |
| 5 | Click the `deleted-bucket-nav-test` hyperlink inside the notification. | Navigation is attempted. |
| 6 | Observe the resulting page and open the browser DevTools Console. | Application does not crash. No unhandled JavaScript exception appears in the console. A graceful fallback is displayed: either a 'Bucket not found' / empty state message, or a redirect to the Artifacts root page without an error dialog. |
| 7 | Close DevTools. Navigate to another page (e.g., Agents) and back to Artifacts. | Application remains fully functional — no broken state, no persistent error overlay. |

## Expected Final State

Application remains fully functional — no broken state, no persistent error overlay.

## Pass/Fail Criteria

**Pass:**
- No application crash or unhandled JS exception after clicking the stale notification link
- A meaningful fallback (empty state, "not found" indicator, or Artifacts root) is displayed
- Application remains operable after the failed navigation

**Fail:**
- Application crashes or shows an unhandled exception / blank screen
- A raw 404/500 error with no application context is displayed
- The application becomes unresponsive or enters a broken navigation state
