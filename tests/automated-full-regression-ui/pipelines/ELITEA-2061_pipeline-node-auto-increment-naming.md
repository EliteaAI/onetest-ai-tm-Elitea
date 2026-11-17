---
id: ELITEA-2061
title: "Pipeline — Node Auto-Increment Naming"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: []
automation_test_id:
  - tests.ui.pipelines_2.test_pipeline_node_auto_increment_naming.test_node_auto_increment_naming_by_type
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1356
---

# ELITEA-2061: Pipeline — Node Auto-Increment Naming

> **Updated for Pipelines 2.0:** title corrected — this case covers auto-increment naming of newly added nodes only. Duplicate node (#7161) is covered by ELITEA-4719.

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify that nodes of the same type are named with incrementing numbers (e.g., "LLM 1", "LLM 2") when added to the pipeline, confirming the auto-naming behavior for multiple nodes of the same type.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline is open in Flow view.

---

## Test Data

| Field | Value |
|-------|-------|
| Node type | LLM (or any repeatable type) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open a pipeline with a configured node | Pipeline is open |
| 2 | Click "+ Node" and add a node of any type (e.g., LLM, Code, Printer) | Node is added |
| 3 | Verify the added node name is "<NodeType> number" (e.g., "LLM 1", "Code 2") | Node name follows the incremental naming pattern |
| 4 | Click "+ Node" and add another node of the same type | Second node of the same type is added |
| 5 | Verify the node name increments (e.g., "LLM 2", "Code 3") | New node name is incremented from the previous |

---

## Expected Final State

Multiple nodes of the same type are named with incrementing numbers, confirming the auto-naming convention (e.g., "LLM 1", "LLM 2", "LLM 3").

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Nodes of the same type have incrementally numbered names.

**Fail:**
- Any step produces an error or unexpected result.
- Node names do not follow the incremental naming pattern.
