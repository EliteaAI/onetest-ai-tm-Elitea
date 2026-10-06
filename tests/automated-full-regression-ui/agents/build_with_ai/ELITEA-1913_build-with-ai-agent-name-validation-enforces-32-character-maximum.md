---
id: ELITEA-1913
title: "Build with AI — agent name validation enforces 32-character maximum"
priority: medium
type: functional
module: agents
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agents]
requirements: []
---

# ELITEA-1913: Build with AI — agent name validation enforces 32-character maximum

**Module:** agents · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Name field in the Build with AI review form enforces a 32-character maximum, displaying a validation error and disabling the Approve button when exceeded, and clearing the error when the name is within the limit.

---

## Preconditions

- User is logged in to the Elitea platform with admin or editor role.
- An agent draft has been generated and the review/edit form is displayed.

---

## Test Data

| Field | Value |
|-------|-------|
| Over-limit name | A string of 33 or more characters |
| Valid name (32 chars) | A string of exactly 32 characters |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Generate an agent draft and enter the review form | The review/edit form is displayed |
| 2 | Edit the Name field to a string exceeding 32 characters | The Name field displays the over-limit text |
| 3 | Verify a validation message is shown for the Name field | A validation error message is displayed near the Name field |
| 4 | Verify the "Approve" / "Create Agent" button is inactive/disabled | The Approve button is disabled and cannot be clicked |
| 5 | Trim the name to exactly 32 characters | The Name field displays the trimmed 32-character name |
| 6 | Verify the validation error clears and the button becomes active | The validation error disappears and the Approve button is enabled |

---

## Expected Final State

The Name field validation enforces the 32-character limit: the Approve button is disabled for over-limit names and enabled once the name is within the allowed length.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Validation error appears for names >32 characters and clears when the name is ≤32 characters.
- The Approve button is disabled/enabled accordingly.

**Fail:**
- Any step produces an error or unexpected result.
- Validation error is not shown for over-limit names, or the Approve button remains active when the name exceeds 32 characters.
