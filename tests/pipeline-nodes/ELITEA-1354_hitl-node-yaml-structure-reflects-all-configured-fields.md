---
id: ELITEA-1354
title: "HITL Node YAML Structure Reflects All Configured Fields"
priority: medium
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1354: HITL Node YAML Structure Reflects All Configured Fields

**Module:** Pipeline Nodes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the YAML representation of a fully configured HITL node includes all fields: Input, USER MESSAGE, ROUTER MAPPING (all three routes), and EDIT STATE KEY.

**Coverage:**
- HITL node YAML block present with correct type identifier
- Input type and value present in YAML
- USER MESSAGE type and value present in YAML
- All three ROUTER MAPPING entries present in YAML
- EDIT STATE KEY present in YAML

## Preconditions

- Pipeline editor with a fully configured HITL node: Input type F-String value {{state.question}}, USER MESSAGE type Variable, ROUTER MAPPING APPROVE node_a EDIT node_b REJECT node_c, EDIT STATE KEY hitl_edit
- YAML view accessible

## Test Data

Input: {{state.question}}; USER MESSAGE variable; Routes: node_a/node_b/node_c; EDIT STATE KEY: hitl_edit

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Switch the pipeline editor to YAML view | YAML representation displayed |
| 2 | Locate the HITL node block (e.g., type hitl) | HITL node block is present in the YAML |
| 3 | Verify Input field: type (f_string) and value ({{state.question}}) | Input configuration block correct |
| 4 | Verify USER MESSAGE: type and variable reference present | user_message block correctly serialized |
| 5 | Verify ROUTER MAPPING: all three routes (APPROVE → node_a, EDIT → node_b, REJECT → node_c) | All three route entries present with correct target node names |
| 6 | Verify EDIT STATE KEY: hitl_edit | edit_state_key: hitl_edit present in YAML block |

## Expected Final State

edit_state_key: hitl_edit present in YAML block

## Pass/Fail Criteria

**Pass:**
- YAML completely and accurately represents all configured HITL node fields

**Fail:**
- Any field missing from YAML
- Incorrect values in YAML
- HITL node block absent from YAML
