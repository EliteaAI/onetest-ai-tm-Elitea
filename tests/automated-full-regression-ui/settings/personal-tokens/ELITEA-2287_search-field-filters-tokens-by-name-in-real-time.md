---
id: ELITEA-2287
title: "Search field filters tokens by name in real time"
priority: medium
type: functional
module: settings-personal-tokens
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:settings]
requirements: []
---

# ELITEA-2287: Search field filters tokens by name in real time

**Module:** settings-personal-tokens · **Priority:** medium · **Type:** functional

**Objective:** Verify that Search field filters tokens by name in real time. Success is confirmed when clear the search field — verify all tokens are shown again.

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
| 1 | Navigate to Settings → Personal Tokens with at least two tokens with different names | Target page/section loads successfully. |
| 2 | Type a partial name in the "Search tokens..." field | Field accepts the input and displays the entered value. |
| 3 | Verify the table filters in real time to show only matching token names | Condition holds as described. |
| 4 | Verify the search is case-insensitive (e.g., "AUTO" matches "autotest-token") | Condition holds as described. |
| 5 | Clear the search field — verify all tokens are shown again | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Clear the search field — verify all tokens are shown again.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Search field filters tokens by name in real time.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
