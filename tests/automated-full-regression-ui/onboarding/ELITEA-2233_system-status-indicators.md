---
id: ELITEA-2233
title: "Onboarding — System Status Indicators"
priority: high
type: functional
module: onboarding
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:onboarding]
requirements: []
---

# ELITEA-2233: Onboarding — System Status Indicators

**Module:** onboarding · **Priority:** high · **Type:** functional

**Objective:** Verify that system status indicators are correctly displayed on first login: green dot on the ELITEA logo (active server connection) and red badge on the bell notification icon (unread notification).

---

## Preconditions

- User is logged in to the Elitea platform for the first time.
- User has navigated to their Private project.

---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in to the Private project of the application for the first time | User is authenticated and lands on the expected landing page. |
| 2 | Locate the ELITEA logo icon in the top left of the sidebar | Action completes without error and produces the expected UI state. |
| 3 | Verify a green dot is displayed above the ELITEA logo | Condition holds as described. |
| 4 | Verify no red dot is shown on the ELITEA logo (red dot would indicate server is updating) | Condition holds as described. |
| 5 | Locate the bell (notification) icon in the top right area of the sidebar header | Action completes without error and produces the expected UI state. |
| 6 | Verify the bell icon is visible | Condition holds as described. |
| 7 | Verify a red badge/dot is displayed above the bell icon | Condition holds as described. |
| 8 | Click the red dot to open the notifications modal | Control responds; modal opens. |
| 9 | Verify the modal displays "Project was successfully created" notification | Condition holds as described. |
| 10 | Click the "X" button to close the modal | Control responds; modal closes. |
| 11 | Verify the Notifications modal closes | Condition holds as described. |

---

## Expected Final State

System status indicators are correctly displayed: green dot on ELITEA logo (indicating active server connection), red badge on bell notification icon (indicating unread notification), and notification modal functions correctly.

---

## Pass/Fail Criteria

**Pass:**
- All assertions verified: Green dot visible on ELITEA logo, no red dot on logo, red badge visible on bell icon, notification modal opens and displays "Project was successfully created", modal closes successfully.

**Fail:**
- Any assertion fails, status indicators are not displayed correctly, or notification modal does not function as expected.

---

## Notes

**Source functional tests:** ELITEA-2233, ELITEA-2234

**Regression rationale:** Consolidated from 2 tests to verify both system status indicators (server connection and notifications) together on first login. This ensures visual status feedback is working correctly for new users.

**Selected checkpoints:** Green dot on ELITEA logo (active connection), absence of red dot on logo, red badge on bell icon, notification modal content ("Project was successfully created"), modal close functionality.
