---
id: ELITEA-0136
title: "Agent Creation - Field Validation"
priority: high
type: functional
module: agents
status: ready
execution_type: manual
automation_test_id: []
tags: []
requirements: []
---
# ELITEA-0136: Agent Creation - Field Validation

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify agent creation form required fields validation.

**Coverage:**
- Create agent form validates required fields (name)
- Validation errors display correctly

## Preconditions

- User is logged in to {{base_url}} via Keycloak
- Browser: Chrome or Chromium

## Test Data

- URL: {{base_url}}
- Partial agent name for testing: autotest_partial

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Agents from the sidebar. Click 'Create Agent' to open the agent creation form. | The create form loads with all fields empty. |
| 2 | Without filling any fields, check whether the Save button is enabled or disabled. | The Save button is disabled (greyed out or not clickable). |
| 3 | Fill only the Name field with 'autotest_partial'. Leave all other fields empty. | The Name field is populated. The Save button may still be disabled if other fields (like Description) are also required. |
| 4 | Check the Save button state with only the Name field filled. | The Save button remains disabled until all required fields are populated. The form does not allow premature submission. |

## Expected Final State

The Save button remains disabled until all required fields are populated. The form does not allow premature submission.

## Pass/Fail Criteria

**Pass:**
- Save button disabled with empty form
- Partial form fill keeps Save disabled
- No premature form submission possible
- Form validation messages display correctly

**Fail:**
- Save button enabled with empty fields
- Form submits with missing required fields
- No visual indication of required fields
- Form allows creation without minimum data
