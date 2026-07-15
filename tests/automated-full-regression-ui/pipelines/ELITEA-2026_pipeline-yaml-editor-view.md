---
id: ELITEA-2026
title: "Pipeline — YAML Editor View"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2026: Pipeline — YAML Editor View

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that the YAML editor view is accessible via the Flow/Yaml toggle, displays the pipeline definition with line numbers and a copy button, and contains valid pipeline definition keywords.

---

## Preconditions

- User is logged in to the Elitea platform.
- An existing pipeline with nodes (e.g., "YAML Validation") is accessible.

---

## Test Data

| Field | Value |
|-------|-------|
| Pipeline name | YAML Validation (or any pipeline with nodes) |
| Expected YAML keywords | entry_point, nodes, state |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open an existing pipeline with nodes (e.g., "YAML Validation") | Pipeline loads in Flow view |
| 2 | In the canvas area, locate the "Flow" / "Yaml" toggle buttons | Toggle group is visible above the canvas |
| 3 | Click "Yaml" button | YAML editor view is activated |
| 4 | Verify YAML editor appears with line numbers (1, 2, 3, ...) | Editor is displayed with line numbers |
| 5 | Verify "Copy yaml code to clipboard" button appears | Copy button is visible in the YAML editor |
| 6 | Verify YAML content contains pipeline definition keywords (entry_point, nodes, state) | YAML text includes all expected keywords |
| 7 | Click "Copy yaml code to clipboard" button | Copy action is triggered |
| 8 | Verify clipboard contains the YAML text (or success feedback shown) | Toast notification or clipboard content confirms the copy |

---

## Expected Final State

The YAML editor view correctly displays the pipeline definition with line numbers, copy button, and valid pipeline YAML content including entry_point, nodes, and state keywords.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- YAML editor is accessible, shows line numbers and copy button, and contains valid pipeline keywords.

**Fail:**
- Any step produces an error or unexpected result.
- YAML editor is inaccessible, copy button is missing, or content lacks required keywords.
