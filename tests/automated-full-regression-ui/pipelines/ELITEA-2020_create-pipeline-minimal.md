---
id: ELITEA-2020
title: "Create Pipeline — Minimal"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines]
requirements: []
---

# ELITEA-2020: Create Pipeline — Minimal

**Module:** pipelines · **Priority:** high · **Type:** functional

**Objective:** Verify that a new pipeline can be created with only the required Name field, and that after saving, the pipeline receives a unique ID and defaults to the "base" version.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists with access to the Pipelines feature.

---

## Test Data

| Field | Value |
|-------|-------|
| Pipeline name | AutoTest_Pipeline |
| Description | Automated test pipeline |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Pipelines section via sidebar button "Pipelines" | Pipelines section loads |
| 2 | Click the "+" button next to "Pipeline" label in the sidebar header area | A new pipeline tab opens with an empty form |
| 3 | In the new pipeline tab, fill in Name field with "AutoTest_Pipeline" | Name field is populated |
| 4 | Fill in Description field with "Automated test pipeline" | Description field is populated |
| 5 | Verify "Save" button becomes enabled after Name is filled | Save button is active/enabled |
| 6 | Click "Save" button | Save request is submitted |
| 7 | Verify pipeline is created — URL changes to include the new pipeline ID | URL updates to include a numeric pipeline ID |
| 8 | Verify "Pipeline ID:" appears in the Information section with a numeric value | Pipeline ID is displayed in the Information section |
| 9 | Verify VERSION dropdown shows "base" | VERSION dropdown defaults to "base" |

---

## Expected Final State

A new pipeline "AutoTest_Pipeline" is created with a unique numeric ID, displayed in the URL and Information section, with the VERSION dropdown defaulting to "base".

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Pipeline is saved, receives a unique ID shown in URL and Information section, and VERSION shows "base".

**Fail:**
- Any step produces an error or unexpected result.
- Pipeline is not saved, ID is not shown, or VERSION does not default to "base".
