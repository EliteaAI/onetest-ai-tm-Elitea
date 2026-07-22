---
id: ELITEA-2453
title: "Run Details — Multiple State Variables of Different Types"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2453: Run Details — Multiple State Variables of Different Types

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that Run Details — Multiple State Variables of Different Types. Success is confirmed when verify each variable is individually expandable.

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
| 1 | Create a pipeline with 4+ state variables: input (default String), messages (default List), custom_text (String), custom_num (Number), custom_list (List), custom_json (Json) | Operation completes successfully; state updates and confirmation is shown. |
| 2 | Configure an LLM node that populates all custom variables with structured output enabled | Action completes without error and produces the expected UI state. |
| 3 | Execute the pipeline | Action completes without error and produces the expected UI state. |
| 4 | Open Run Details, select a node step | Target page/section loads successfully. |
| 5 | Verify all state variables appear in STATES section (displayed uppercase) | Condition holds as described. |
| 6 | Expand each variable — verify: | Action completes without error and produces the expected UI state. |
| 7 | INPUT: shows string value in Before/After | Field accepts the input and displays the entered value. |
| 8 | MESSAGES: shows list representation in Before/After | Action completes without error and produces the expected UI state. |
| 9 | CUSTOM_TEXT: shows string values | Action completes without error and produces the expected UI state. |
| 10 | CUSTOM_NUM: shows numeric values | Action completes without error and produces the expected UI state. |
| 11 | CUSTOM_LIST: shows list/array representation | Action completes without error and produces the expected UI state. |
| 12 | CUSTOM_JSON: shows JSON object representation | Action completes without error and produces the expected UI state. |
| 13 | Verify each variable is individually expandable | Condition holds as described. |

---

## Expected Final State

Verify each variable is individually expandable.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Run Details — Multiple State Variables of Different Types.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
