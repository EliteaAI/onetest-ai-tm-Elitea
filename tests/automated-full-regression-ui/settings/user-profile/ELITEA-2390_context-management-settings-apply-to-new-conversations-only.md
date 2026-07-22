---
id: ELITEA-2390
title: "Context management settings apply to new conversations only"
priority: high
type: functional
module: settings-user-profile
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2390: Context management settings apply to new conversations only

**Module:** settings-user-profile · **Priority:** high · **Type:** functional

**Objective:** Verify that Context management settings apply to new conversations only. Success is confirmed when verify its context management settings remain unchanged.

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
| 1 | Navigate to Settings → Personalization → DEFAULT CONTEXT MANAGEMENT | Target page/section loads successfully. |
| 2 | Enable context management and set Max Context Tokens to 32000 and Preserve Recent Messages to 3 | Action completes without error and produces the expected UI state. |
| 3 | Navigate away and back to confirm values were auto-saved | Target page/section loads successfully. |
| 4 | Create a new conversation | Operation completes successfully; state updates and confirmation is shown. |
| 5 | Verify the new conversation has context management active with the configured values | Condition holds as described. |
| 6 | Open a previously existing conversation | Target page/section loads successfully. |
| 7 | Verify its context management settings remain unchanged | Condition holds as described. |

---

## Expected Final State

Verify its context management settings remain unchanged.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Context management settings apply to new conversations only.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
