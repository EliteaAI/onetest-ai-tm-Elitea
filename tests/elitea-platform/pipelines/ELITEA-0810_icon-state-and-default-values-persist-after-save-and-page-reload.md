---
id: ELITEA-0810
title: "Icon state and default values persist after save and page reload"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [issue:2676, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2676]
---
# ELITEA-0810: Icon state and default values persist after save and page reload

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that after configuring default values and saving the pipeline, the correct icons (≡ for variables with defaults, + for those without) and the configured values persist after a page reload.

**Coverage:**
- ≡ icons persist after save and reload for variables with defaults
- + icons persist after reload for variables without defaults
- Configured values are intact after reload

## Preconditions

- Logged in to {{base_url}} with a valid user account
- A Pipeline with a mix of variables: some with default values (showing ≡) and some without (showing +)

## Test Data

- Mix of variables: some with configured default values, some empty

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Pipeline. Open the STATE panel in collapsed view. Note which variables show ≡ and which show +. | Variable icons visible as expected. |
| 2 | Save the pipeline using the Save button. | Pipeline saved successfully. |
| 3 | Reload the page. Open the pipeline again and open the STATE panel. | Pipeline reopens. |
| 4 | Verify variables that had default values still show ≡ icon. | ≡ icon present on all variables that had defaults configured. |
| 5 | Verify variables that had no default value still show + icon. | + icon present on all variables without defaults. |
| 6 | Expand a variable that shows ≡ to verify the value is intact. | Inline field shows the configured default value — not empty. |

## Expected Final State

Inline field shows the configured default value — not empty.

## Pass/Fail Criteria

**Pass:**
- Icons and values correct and fully intact after save and reload

**Fail:**
- Icons reset to + for all variables after reload; values lost
