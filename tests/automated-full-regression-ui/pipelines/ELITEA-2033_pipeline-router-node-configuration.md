---
id: ELITEA-2033
title: "Pipeline — Router Node Configuration"
priority: high
type: functional
module: pipelines
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
automation_test_id:
  - tests.ui.pipelines.test_pipeline_router_node_configuration.test_router_node_configuration_and_edge_wiring
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1146
---

# ELITEA-2033: Pipeline — Router Node Configuration

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that a Router node can be configured with a Jinja condition, routes, input variable, and default output, and that the canvas shows edges to target nodes and all configuration persists after save and reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline with state variable "input" and target nodes for routing exists.

---

## Test Data

| Field | Value |
|-------|-------|
| Condition (Jinja) | {% if 'yes' in input %}approve{% else %}reject{% endif %} |
| Routes | approve, reject |
| Input variable | input |
| Default output | END |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a pipeline and add a Router node via "Add node" → "Router" | Router node appears on canvas |
| 2 | Verify Router node panel shows: Condition (Jinja template text area), Routes (combobox), Input combobox, Default output dropdown | All listed sections are present |
| 3 | In "Condition" field enter Jinja template: "{% if 'yes' in input %}approve{% else %}reject{% endif %}" | Condition field accepts the Jinja template |
| 4 | In Routes combobox add route values: "approve", "reject" | Both route values are added |
| 5 | Set Input combobox to state variable "input" | Input is set to "input" variable |
| 6 | Set "Default output" dropdown to "END" | Default output is set to END |
| 7 | Save pipeline | Pipeline saves without errors |
| 8 | Reload — verify Condition text, Routes values, Input, and Default output persist | All Router node fields are correctly restored after reload |
| 9 | Verify canvas shows edges from Router to target nodes matching route values | Edges connect Router to "approve" and "reject" target nodes |

---

## Expected Final State

The Router node is fully configured with Jinja condition, routes ("approve", "reject"), Input "input", and Default output "END", all persisting after save and reload. Canvas edges reflect the configured routes.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All Router node fields persist after reload and canvas shows correct edges.

**Fail:**
- Any step produces an error or unexpected result.
- Any field is lost after saving, or canvas edges do not match configured routes.
