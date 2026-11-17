---
id: ELITEA-4701
title: "Existing Pipelines — Zero-change Guarantee on Open, Click-through and Save"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines, epic:7093, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7156, EliteaAI/elitea_issues#7157, EliteaAI/elitea_issues#7159, EliteaAI/elitea_issues#7160]
---
# ELITEA-4701: Existing Pipelines — Zero-change Guarantee on Open, Click-through and Save

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Verify that pipelines created before Pipelines Editor 2.0 open in the new style without any data change: clicking through every node, saving without edits, and a rename round-trip leave YAML, positions, orientation, attachments, versions and tool restrictions identical.

**Coverage:**
- Existing pipelines render in the new card style (incl. deprecated nodes and End)
- Save stays disabled with no edits
- Opening/closing panels writes no defaults to YAML
- Rename → save → rename back → save is byte-identical
- Positions, orientation, attachments, versions, tool restrictions unchanged
- Pipeline runs as before with run-state highlighting

## Preconditions

- Logged in to {{base_url}}
- An existing pipeline (created before this release) with every node type, a deprecated node, an interrupt, a trigger, attached toolkits/MCPs/agents and a Router referencing another node

## Test Data

- None

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Yaml tab and copy the full YAML as a baseline. | Baseline captured. |
| 2 | Return to Flow. Observe all cards. | All nodes render in the new card style; deprecated node shows its Deprecated badge; End renders as the compact pill. |
| 3 | Observe node positions and orientation. | Saved positions and orientation are shown exactly; Arrange is not auto-triggered. |
| 4 | Observe Save. | Disabled (no changes). |
| 5 | Click every node to open its panel, then close it. | Save stays disabled; no default values are written into the YAML. |
| 6 | Rename a node referenced by the Router; Save; rename it back to the original; Save. | Saves succeed. |
| 7 | Compare the current YAML with the baseline. | Identical. |
| 8 | Observe the TOOLS section. | Attachments, versions and selected tools are unchanged. |
| 9 | Run the pipeline. | Runs as before; run-state highlighting displays on the new cards. |
| 10 | Observe the Router after the rename in step 6. | Note: the Router's displayed route label may show the old name until the dropdown is reopened; the underlying reference is correct. |

## Expected Final State

Existing pipelines are visually migrated to the new style with zero data change; a no-edit save and a rename round-trip produce identical YAML.

## Pass/Fail Criteria

**Pass:**
- New card style applied; deprecated nodes and End render correctly
- Save stays disabled without edits; no defaults written on panel open/close
- Round-trip YAML identical to baseline
- Positions, orientation, attachments, versions and tool restrictions unchanged
- Pipeline runs as before

**Fail:**
- Any YAML, position, orientation or attachment drift
- Save becomes enabled without edits
- Run behaviour or highlighting changes
