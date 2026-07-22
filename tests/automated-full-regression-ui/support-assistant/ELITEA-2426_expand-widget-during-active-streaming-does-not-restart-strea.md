---
id: ELITEA-2426
title: "Expand widget during active streaming does not restart stream"
priority: medium
type: functional
module: support-assistant
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:support-assistant]
requirements: []
---

# ELITEA-2426: Expand widget during active streaming does not restart stream

**Module:** support-assistant · **Priority:** medium · **Type:** functional

**Objective:** Verify that Expand widget during active streaming does not restart stream. Success is confirmed when verify the response completes normally in full-view mode ------if automatable------.

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
| 1 | Open the Support Assistant widget in compact/widget mode | Target page/section loads successfully. |
| 2 | Send a prompt that produces a long response: "List all ELITEA toolkits and describe each one" | Action completes without error and produces the expected UI state. |
| 3 | While the response is actively streaming, click the Expand (↗) button to switch to full-view mode | Action completes without error and produces the expected UI state. |
| 4 | Verify the response stream continues from where it was — it does NOT restart from the beginning | Condition holds as described. |
| 5 | Verify no previously streamed tokens are lost after expanding | Condition holds as described. |
| 6 | Verify the response completes normally in full-view mode ------If automatable------ | Condition holds as described. |

---

## Expected Final State

Verify the response completes normally in full-view mode ------If automatable------.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Expand widget during active streaming does not restart stream.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
