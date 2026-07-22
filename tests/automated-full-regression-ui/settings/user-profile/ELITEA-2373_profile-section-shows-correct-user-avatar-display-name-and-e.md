---
id: ELITEA-2373
title: "Profile section shows correct user avatar, display name, and email"
priority: medium
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2373: Profile section shows correct user avatar, display name, and email

**Module:** settings-user-profile · **Priority:** medium · **Type:** functional

**Objective:** Verify that Profile section shows correct user avatar, display name, and email. Success is confirmed when verify the email matches the logged-in user's email address.

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
| 1 | Navigate to Personalization | Target page/section loads successfully. |
| 2 | Verify the avatar image is shown (not a broken image icon) | Condition holds as described. |
| 3 | Verify the display name matches the logged-in user's name | Condition holds as described. |
| 4 | Verify the email matches the logged-in user's email address | Condition holds as described. |

---

## Expected Final State

Verify the email matches the logged-in user's email address.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Profile section shows correct user avatar, display name, and email.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
