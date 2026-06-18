---
id: ELITEA-0775
title: "Clicking the Bucket Name in an Expiration Notification Navigates to That Bucket's Artifacts Page"
priority: critical
type: functional
module: notifications
status: ready
execution_type: manual
tags: [user_story:3414, feat:artifacts, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3414]
---
# ELITEA-0775: Clicking the Bucket Name in an Expiration Notification Navigates to That Bucket's Artifacts Page

**Module:** Notifications · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the bucket name in a bucket expiration notification is rendered as a clickable hyperlink and navigates the user directly to the correct bucket on the Artifacts page.

**Coverage:**
- Bucket name visually rendered as a hyperlink (underlined/styled) inside the notification
- Clicking navigates to the Artifacts page with the correct bucket selected in the sidebar
- Correct bucket's file contents are displayed after navigation (not another bucket)
- Navigation works when triggered from a non-Artifacts page

## Preconditions

- Logged in to {{base_url}} as the bucket creator
- Browser: Chrome (latest)

## Test Data

- Bucket to test: `nav-click-test`; Retention: Days, Value: 3
- Control bucket (must also exist): `other-bucket`; Retention: Days, Value: 10
- Both buckets created by the same user in the same project

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Artifacts. Confirm `other-bucket` exists in the sidebar. Click '+ Create Bucket'. Enter name: `nav-click-test`, Period Type: Days, Value: 3. Click Save. | `nav-click-test` appears in the sidebar. `other-bucket` is also visible. Immediate expiration notification is triggered. |
| 2 | Navigate away from Artifacts — click a different section in the sidebar (e.g., Agents). | Agents page loads. User is no longer on the Artifacts page. |
| 3 | Click the bell icon in the top navigation bar to open the Notification Center. | Notification Center opens. A notification for `nav-click-test` is visible. |
| 4 | Inspect the bucket name `nav-click-test` inside the notification — hover over it or visually check its styling. | The bucket name is underlined or otherwise visually styled as a clickable hyperlink, not plain text. |
| 5 | Click the `nav-click-test` link inside the notification. | Navigation occurs. The browser URL changes to the Artifacts route. |
| 6 | Verify that `nav-click-test` is highlighted/selected in the Artifacts sidebar (not `other-bucket`). | `nav-click-test` is the active selected bucket in the sidebar. `other-bucket` is not selected. |
| 7 | Verify that the main content area displays the file contents (or empty state) of `nav-click-test`. | Correct bucket content area is shown. No error, no blank page. |

## Expected Final State

Correct bucket content area is shown. No error, no blank page.

## Pass/Fail Criteria

**Pass:**
- Bucket name in notification is a visually distinct clickable hyperlink
- Clicking navigates to Artifacts with `nav-click-test` selected
- Correct bucket contents displayed after navigation
- No errors during navigation

**Fail:**
- Bucket name is plain unclickable text
- Navigation opens Artifacts without selecting the correct bucket, or selects `other-bucket`
- Navigation results in a 404 or error page
