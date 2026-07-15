---
id: ELITEA-2034
title: "Pipeline — Decision Node Configuration"
priority: high
type: functional
module: pipelines
status: draft
execution_type: automated
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2034: Pipeline — Decision Node Configuration

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that a Decision node can be fully configured with input variables, classification description, and DECISION OUTPUTS, and that all configuration persists after save and reload with correct output handles on the canvas.

---

## Preconditions

- User is logged in to the Elitea platform.
- A pipeline with state variables and branch nodes exists.

---

## Test Data

| Field | Value |
|-------|-------|
| Input variables | normalized_issue, metadata_json |
| Classification prompt | Classify this input into one category: - bug_responder: reports a defect - feature_responder: requests new functionality |
| DECISION OUTPUTS | bug_responder, feature_responder, question_responder |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create a pipeline and add a Decision node via "Add node" → "Decision" | Decision node appears on canvas |
| 2 | Verify Decision node panel shows: Input combobox, Description text area, DECISION OUTPUTS (chip-style list), Interrupt before/after switches | All listed sections are present |
| 3 | Set Input combobox with state variables: "normalized_issue", "metadata_json" | Both variables are added to Input |
| 4 | Fill Description with classification prompt | Description field accepts the classification text |
| 5 | In DECISION OUTPUTS: add target node names as chips: "bug_responder", "feature_responder", "question_responder" | All three output chips are added |
| 6 | Save pipeline | Pipeline saves without errors |
| 7 | Reload — verify Input variables, Description text, and DECISION OUTPUTS chips persist | All Decision node fields are correctly restored after reload |
| 8 | Verify canvas shows two output handles: "Output" and "Default output" at bottom of node | Both output handles are visible on the Decision node |

---

## Expected Final State

The Decision node is fully configured with input variables, classification description, and three DECISION OUTPUTS, all persisting after save and reload. The node shows "Output" and "Default output" handles on the canvas.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- All Decision node fields persist after reload and canvas shows correct output handles.

**Fail:**
- Any step produces an error or unexpected result.
- Any field is lost after saving, or canvas output handles are missing.
