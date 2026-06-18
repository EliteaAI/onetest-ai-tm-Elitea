---
id: ELITEA-1359
title: "HITL Node Router Mapping: Collapse/Expand Retains Configured Values"
priority: medium
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1359: HITL Node Router Mapping: Collapse/Expand Retains Configured Values

**Module:** Pipeline Nodes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the ROUTER MAPPING section retains all configured route values when collapsed and re-expanded, and after save.

**Coverage:**
- APPROVE, EDIT, REJECT values preserved through collapse/expand
- Values persist after pipeline save and re-open

## Preconditions

- Pipeline editor open; HITL node configuration panel open
- ROUTER MAPPING section visible

## Test Data

Approve route label: approve_node; Edit route label: edit_node; Reject route label: reject_node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Expand the ROUTER MAPPING section | Three route fields (APPROVE, EDIT, REJECT) visible |
| 2 | Enter values: Approve = approve_node, Edit = edit_node, Reject = reject_node | All three values entered |
| 3 | Collapse the ROUTER MAPPING section | Section collapses |
| 4 | Expand the ROUTER MAPPING section again | All three route values still present — no data loss |
| 5 | Save the pipeline and re-open the HITL configuration panel | ROUTER MAPPING values are persisted after save and re-open |

## Expected Final State

ROUTER MAPPING values are persisted after save and re-open

## Pass/Fail Criteria

**Pass:**
- Values preserved through collapse/expand and save/re-open

**Fail:**
- Values reset to empty on collapse/expand
- Values not persisted after save
