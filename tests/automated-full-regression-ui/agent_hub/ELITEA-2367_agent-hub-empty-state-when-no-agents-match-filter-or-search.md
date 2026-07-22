---
id: ELITEA-2367
title: "Agent Hub — empty state when no agents match filter or search"
priority: high
type: functional
module: agent-hub
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:agent-hub]
requirements: []
---

# ELITEA-2367: Agent Hub — empty state when no agents match filter or search

**Module:** agent-hub · **Priority:** high · **Type:** functional

**Objective:** Verify that Agent Hub — empty state when no agents match filter or search. Success is confirmed when verify the layout remains consistent with no broken ui elements.

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
| 1 | Navigate to Agent Hub | Target page/section loads successfully. |
| 2 | Apply a category filter that has no agents OR type a search term that matches no agents | Operation completes successfully; state updates and confirmation is shown. |
| 3 | Verify the "No agents found" message is displayed in the main content area | Condition holds as described. |
| 4 | Verify a helper message appears (e.g., "Try adjusting your search terms") | Condition holds as described. |
| 5 | Verify the layout remains consistent with no broken UI elements | Condition holds as described. |

---

## Expected Final State

Verify the layout remains consistent with no broken UI elements.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Agent Hub — empty state when no agents match filter or search.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
