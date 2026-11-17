---
id: ELITEA-2033
title: "Pipeline — Router Node Configuration"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7157]
---

# ELITEA-2033: Pipeline — Router Node Configuration

> **Updated for Pipelines 2.0:** wording modernized — the node is added via "+ Node" and configured in the node configuration panel (cards are view-only). Checks unchanged.

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that a Router node can be configured with a Jinja condition, routes, input variable, and default output, and that the canvas shows edges to target nodes and all configuration persists after save and reload.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline with state variable "input" and two target nodes named "approve" and "reject" exists.

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
| 1 | Open the pipeline; click "+ Node" and select "Router" | Router node card "Router 1" appears on the canvas |
| 2 | Click the "Router 1" card | The node configuration panel opens and shows: Condition (Jinja text area), Routes (combobox), Input combobox, Default output dropdown |
| 3 | In "Condition" enter: {% if 'yes' in input %}approve{% else %}reject{% endif %} | Condition field accepts the Jinja template |
| 4 | In the Routes combobox add "approve" and "reject" | Both route values are added |
| 5 | Set the Input combobox to "input" | Input is set to "input" |
| 6 | Set "Default output" to "END" | Default output is set to END |
| 7 | Click "Save" | Pipeline saves without errors |
| 8 | Reload; click the "Router 1" card | Condition text, Routes values, Input and Default output are restored in the panel |
| 9 | Inspect the canvas | Edges connect "Router 1" to the "approve" and "reject" target nodes |

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
