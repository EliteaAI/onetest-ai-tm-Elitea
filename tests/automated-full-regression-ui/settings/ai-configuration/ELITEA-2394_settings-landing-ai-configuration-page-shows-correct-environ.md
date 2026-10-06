---
id: ELITEA-2394
title: "Settings landing — AI Configuration page shows correct environment metadata fields"
priority: high
type: functional
module: settings-ai-configuration
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2394: Settings landing — AI Configuration page shows correct environment metadata fields

**Module:** settings-ai-configuration · **Priority:** high · **Type:** functional

**Objective:** Verify that Settings landing — AI Configuration page shows correct environment metadata fields. Success is confirmed when verify none of the values show "undefined", blank, or a permanent loading spinner.

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
| 1 | Log in as a user with Admin role | User is authenticated and lands on the expected landing page. |
| 2 | Click "Settings" in the left sidebar | Control responds; expected next state is shown. |
| 3 | Verify "AI Configuration" is selected and active by default | Condition holds as described. |
| 4 | Verify the main content area shows the following fields with non-empty values: | Condition holds as described. |
| 5 | OpenAI-BaseURL | Action completes without error and produces the expected UI state. |
| 6 | Server URL | Action completes without error and produces the expected UI state. |
| 7 | OpenAI-Project | Action completes without error and produces the expected UI state. |
| 8 | Project ID | Action completes without error and produces the expected UI state. |
| 9 | Verify none of the values show "undefined", blank, or a permanent loading spinner | Condition holds as described. |

---

## Expected Final State

Verify none of the values show "undefined", blank, or a permanent loading spinner.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Settings landing — AI Configuration page shows correct environment metadata fields.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
