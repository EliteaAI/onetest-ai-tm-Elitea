---
id: ELITEA-2251
title: "Settings — sections show loading state while data is being fetched"
priority: high
type: functional
module: settings
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:settings]
requirements: []
automation_test_id:
  - tests.ui.settings.test_ai_providers_sections_loading_state.TestAIProvidersSectionsLoadingState.test_ai_providers_sections_loading_state
automation_pr: "https://github.com/EliteaAI/elitea-testing-public/pull/1779"
---

# ELITEA-2251: Settings — sections show loading state while data is being fetched

**Module:** settings · **Priority:** high · **Type:** functional

**Objective:** Verify that Settings — sections show loading state while data is being fetched. Success is confirmed when verify the page does not remain in a permanent loading state.

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
| 1 | Navigate to Settings → AI Configuration on a slow or throttled connection | Target page/section loads successfully. |
| 2 | Verify a loading indicator is shown while configurations are loading | Condition holds as described. |
| 3 | Verify the loading indicator disappears once data is fully loaded | Condition holds as described. |
| 4 | Verify the page does not remain in a permanent loading state | Condition holds as described. |

---

## Expected Final State

Verify the page does not remain in a permanent loading state.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Settings — sections show loading state while data is being fetched.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
