---
id: ELITEA-4721
title: "Pipeline — Viewer Role Has a Read-Only Pipeline Editor"
priority: critical
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7157, EliteaAI/elitea_issues#7158, EliteaAI/elitea_issues#7159, EliteaAI/elitea_issues#7161, EliteaAI/elitea_issues#7407]
---

# ELITEA-4721: Pipeline — Viewer Role Has a Read-Only Pipeline Editor

**Module:** pipelines · **Priority:** critical · **Type:** functional

**Objective:** Verify that a user with the Viewer role cannot change a pipeline: save actions are hidden, node panel fields and node YAML are read-only, Replace and Duplicate are unavailable, and pickers cannot attach tools.

---

## Preconditions

- A separate user account with the **Viewer** role in the same project as the pipeline.
- A saved pipeline in that project with an "Agent 1" (Agent, entry point) node and a "Toolkit 1" (Toolkit) node, both configured.

---

## Test Data

| Field | Value |
|-------|-------|
| User | Viewer-role account |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Log in as the Viewer user; open the pipeline | The pipeline opens. "Save", "Save As Version" and "Discard" are not shown |
| 2 | Click the "Agent 1" card | The configuration panel opens. Name, Agents & Pipelines picker, Version, Task and all other fields are disabled / non-editable |
| 3 | Try to type in the Name field | The value does not change |
| 4 | Switch the panel to "YAML" and try to type in the editor | The editor is read-only; the content does not change |
| 5 | Press Ctrl+F and search for `transition` | Find works |
| 6 | Press Ctrl+H | Replace is disabled / not available |
| 7 | Click the Copy icon in the editor | YAML is copied |
| 8 | Check the panel footer | The Duplicate and Delete icons are hidden — not present in the footer (Make Entrypoint also not available) |
| 9 | Open "Toolkit 1" and try to open the Toolkit picker | The picker cannot be opened or no selection can be made; the TOOLS section (left side panel) does not change |

---

## Expected Final State

The Viewer can inspect the pipeline (panels, YAML, Find, Copy) but cannot make any change.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- No field, YAML, Replace, Duplicate or picker action can modify the pipeline for the Viewer.

**Fail:**
- Save / Save As Version / Discard is shown to the Viewer.
- Any field, the node YAML, Replace, Duplicate or a picker allows a change.

**Notes:** Regression for EliteaAI/elitea_issues#7407 (fixed). Step 1 also covers ELITEA-4375.
