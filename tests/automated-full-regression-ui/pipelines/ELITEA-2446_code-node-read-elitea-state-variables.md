---
id: ELITEA-2446
title: "Code Node — Read elitea_state Variables"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines.test_pipeline_code_node_reads_state_variable.test_code_node_reads_elitea_state_variable
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/96d8e21b
---

# ELITEA-2446: Code Node — Read elitea_state Variables

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that Code Node — Read elitea_state Variables. Success is confirmed when open yaml editor — verify code node shows input: [user_info] and output: code_output.

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
| 1 | Create a pipeline with state variable user_info (String) | Operation completes successfully; state updates and confirmation is shown. |
| 2 | Add two nodes: LLM node (sets user_info) → Code node → END | Operation completes successfully; state updates and confirmation is shown. |
| 3 | In Code node, set Input combobox to include user_info | Action completes without error and produces the expected UI state. |
| 4 | In Code node script, read from elitea_state: result = elitea_state.get('user_info', '') output = f"Processed: {result}" output | Action completes without error and produces the expected UI state. |
| 5 | Set Code node Output to a state variable (e.g., code_output) | Action completes without error and produces the expected UI state. |
| 6 | Enable the structured output | Action completes without error and produces the expected UI state. |
| 7 | Execute the pipeline | Action completes without error and produces the expected UI state. |
| 8 | Open Run Details, click on the Code node step | Run Details timeline step label shows the Code node's own name (e.g. "Code1"), not the sandbox name. |
| 9 | Verify code_output After value contains the processed user_info value | Condition holds as described. |
| 10 | Verify no execution errors in timeline | Condition holds as described. |
| 11 | Open YAML editor — verify Code node shows input: [user_info] and output: code_output | Target page/section loads successfully. |

---

## Expected Final State

Open YAML editor — verify Code node shows input: [user_info] and output: code_output.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Code Node — Read elitea_state Variables.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
