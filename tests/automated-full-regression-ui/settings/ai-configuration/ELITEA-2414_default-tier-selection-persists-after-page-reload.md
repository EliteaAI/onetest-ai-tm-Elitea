---
id: ELITEA-2414
title: "Default tier selection persists after page reload"
priority: medium
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2414: Default tier selection persists after page reload

**Module:** settings-ai-configuration · **Priority:** medium · **Type:** functional

**Objective:** Verify that Default tier selection persists after page reload. Success is confirmed when verify the default selector still shows the model selected in step 2.

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
| 1 | Navigate to Settings → AI Configuration | Target page/section loads successfully. |
| 2 | Change the Default LLM model selector to a different model | Action completes without error and produces the expected UI state. |
| 3 | Reload the page | Action completes without error and produces the expected UI state. |
| 4 | Verify the Default selector still shows the model selected in step 2 | Condition holds as described. |

---

## Expected Final State

Verify the Default selector still shows the model selected in step 2.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Default tier selection persists after page reload.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
