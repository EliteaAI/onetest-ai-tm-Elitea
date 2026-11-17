---
id: ELITEA-0926
title: "Verify Pipeline Creation and Editing Workflow — Full Regression"
priority: critical
type: functional
module: pipeline-creation-ux
status: draft
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418, epic:7093]
requirements: [EliteaAI/elitea_issues#4418, EliteaAI/elitea_issues#7154, EliteaAI/elitea_issues#7159]
---
# ELITEA-0926: Verify Pipeline Creation and Editing Workflow — Full Regression

> **Updated for Pipelines 2.0:** Creation is canvas-first and only Name is required (#7154). The TOOLS section is read-only and tools are picked inside nodes (#7159), so the "+Toolkit" steps are replaced by the node picker.

**Module:** Pipeline Creation Ux · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the end-to-end pipeline creation and editing workflow — canvas-first creation, save, Flow editor, YAML editor and the read-only TOOLS section.

**Coverage:**
- End-to-end pipeline creation regression
- Flow and YAML editors usable before and after the first save
- Tool picked in a node appears in the read-only TOOLS section
- Edit existing pipeline — all sections accessible

## Preconditions

- Logged in
- Private project selected
- At least one toolkit exists in the project

## Test Data

- Pipeline Name: TC15-E2E-Regression-Pipeline
- Description: End to end regression test TC15 (optional)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Pipelines section | Pipelines list is displayed |
| 2 | Click **+ Pipeline** | The new pipeline opens on the canvas with the empty-state card and the **+ Add Node** button. Flow / Yaml toggle is available |
| 3 | Set Name "TC15-E2E-Regression-Pipeline" and Description. Click Save | Pipeline is saved. The editor stays on the canvas |
| 4 | Click **+ Add Node** and add a Toolkit node | The node is added as the entry point. End appears |
| 5 | Click the Toolkit node card | The node configuration panel opens on the right |
| 6 | In the panel's Toolkit picker, select a project toolkit | The toolkit is auto-attached and appears in the left **TOOLS** section with "Used by: <node name>". There are no "+ Toolkit / + MCP" buttons in TOOLS |
| 7 | Switch to **Yaml** | The YAML editor displays the pipeline YAML including the node and its `toolkit_name` |
| 8 | Save. Navigate back to the Pipelines list, then re-open the pipeline | Pipeline opens with Flow, Yaml and TOOLS all available and the node configuration intact |
| 9 | Make a minor edit (e.g. update Welcome Message) and Save | Edit saves without error |

## Expected Final State

The pipeline is created, edited and re-opened without errors; the picked toolkit is shown in TOOLS.

## Pass/Fail Criteria

**Pass:**
- Full create-save-edit cycle completes without error
- Flow editor, YAML editor and TOOLS section are functional
- Tool picked in the node auto-appears in TOOLS
- Re-opening for edit keeps all sections and configuration

**Fail:**
- Any stage of the create or edit flow fails
- Flow/YAML editor is non-functional
- Picked tool does not appear in TOOLS, or "+ Toolkit / + MCP" buttons are still present
