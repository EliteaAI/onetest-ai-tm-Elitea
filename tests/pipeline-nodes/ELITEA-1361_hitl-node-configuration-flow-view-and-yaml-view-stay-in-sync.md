---
id: ELITEA-1361
title: "HITL Node Configuration: Flow View and YAML View Stay in Sync"
priority: medium
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1361: HITL Node Configuration: Flow View and YAML View Stay in Sync

**Module:** Pipeline Nodes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that changes made to the HITL node in Flow view are correctly reflected in YAML view, and vice versa.

**Coverage:**
- Flow → YAML sync for all configured fields
- YAML → Flow sync for an edited field

## Preconditions

- Pipeline editor open with HITL node; all fields configured

## Test Data

Input type: F-String, value: {{state.input}}; USER MESSAGE type: Fixed, value: Please review; EDIT STATE KEY: review_feedback

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | In Flow view, configure HITL node with the test data values | All values entered in Flow view configuration panel |
| 2 | Switch to YAML view | YAML representation is shown |
| 3 | Locate the HITL node section in the YAML | HITL node block contains all configured values: input type/value, user_message, edit_state_key |
| 4 | In YAML view, change USER MESSAGE value to 'Please verify' and save | YAML change saved |
| 5 | Switch back to Flow view; open HITL configuration panel | USER MESSAGE value shows 'Please verify' — YAML edit reflected in Flow view |

## Expected Final State

USER MESSAGE value shows 'Please verify' — YAML edit reflected in Flow view

## Pass/Fail Criteria

**Pass:**
- Flow → YAML and YAML → Flow remain in sync

**Fail:**
- YAML and Flow views show different values
- HITL block missing from YAML
