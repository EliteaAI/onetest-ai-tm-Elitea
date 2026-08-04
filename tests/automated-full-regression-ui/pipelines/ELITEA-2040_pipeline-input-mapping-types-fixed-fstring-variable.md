---
id: ELITEA-2040
title: "Pipeline — Input Mapping Types (Fixed, F-String, Variable)"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines.test_pipeline_llm_node_system_task_chat_history_config.test_llm_node_system_type_walks_fixed_fstring_variable
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1153
---

# ELITEA-2040: Pipeline — Input Mapping Types (Fixed, F-String, Variable)

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that all three input mapping types (Fixed, F-String, Variable) are selectable in node configuration panels and that the selected type and value persist correctly after save and reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline with a node that has Type+Value fields (e.g., LLM node SYSTEM section) exists.

---

## Test Data

| Field | Value |
|-------|-------|
| Fixed value | Extract these four values from the given input |
| F-String value | input: {input} |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline with a node that has Type+Value fields (e.g., LLM node SYSTEM section) | Pipeline is open with a node having Type+Value fields |
| 2 | Locate any Type dropdown (appears in SYSTEM, TASK, CHAT HISTORY, CODE, PRINTER, INPUT MAPPING sections) | Type dropdown is visible |
| 3 | Set Type dropdown to "Fixed" — verify Value field accepts plain text (static content) | Value field accepts plain text input |
| 4 | Enter a fixed value: "Extract these four values from the given input" | Value field shows the entered text |
| 5 | Change Type to "F-String" — verify Value field allows {variable} syntax | Value field accepts f-string interpolation syntax |
| 6 | Enter value: "input: {input}" — confirms f-string interpolation format | Value field shows the f-string value |
| 7 | Change Type to "Variable" — verify Value field changes behavior (references state variable directly) | Value field behavior changes to variable reference mode |
| 8 | Save pipeline | Pipeline saves without errors |
| 9 | Reload — verify selected Type and Value persist correctly | Type and Value are correctly restored after reload |

---

## Expected Final State

All three input mapping types (Fixed, F-String, Variable) are functional. The selected type and corresponding value persist correctly after save and reload.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All three Type options are available and selectable; selected Type and Value persist after reload.

**Fail:**
- Any step produces an error or unexpected result.
- A Type option is missing, or Type/Value does not persist after saving.
