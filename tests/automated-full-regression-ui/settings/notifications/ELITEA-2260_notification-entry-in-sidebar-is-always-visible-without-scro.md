---
id: ELITEA-2260
title: "Notification entry in sidebar is always visible without scrolling"
priority: medium
type: functional
module: settings-notifications
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2260: Notification entry in sidebar is always visible without scrolling

**Module:** settings-notifications · **Priority:** medium · **Type:** functional

**Objective:** Verify that Notification entry in sidebar is always visible without scrolling. Success is confirmed when verify any unread count badge is displayed next to "notifications".

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as any user | User is authenticated and lands on the expected landing page. |
| 2 | Navigate to any Settings sub-page | Target page/section loads successfully. |
| 3 | Verify "Notifications" is visible in the PERSONAL section of the sidebar without scrolling | Condition holds as described. |
| 4 | Verify any unread count badge is displayed next to "Notifications" | Condition holds as described. |

---

## Expected Final State

Verify any unread count badge is displayed next to "Notifications".

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Notification entry in sidebar is always visible without scrolling.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
