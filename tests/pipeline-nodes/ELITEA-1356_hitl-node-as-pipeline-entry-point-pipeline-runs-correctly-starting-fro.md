---
id: ELITEA-1356
title: "HITL Node as Pipeline Entry Point: Pipeline Runs Correctly Starting From HITL"
priority: high
type: functional
module: pipeline-nodes
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, user_story:3471, feat:pipelines, r-2.0.1, 3471]
requirements: [ProjectAlita/projectalita.github.io#3471]
---
# ELITEA-1356: HITL Node as Pipeline Entry Point: Pipeline Runs Correctly Starting From HITL

**Module:** Pipeline Nodes · **Priority:** High · **Type:** Functional

**Objective:** Verify that a pipeline with the HITL node designated as the entry point starts execution from HITL and pauses for a human decision before any other node runs.

**Coverage:**
- HITL node entry point designation
- Pipeline execution starts with HITL pause (first action is human decision)
- Downstream nodes execute after decision

## Preconditions

- Pipeline with HITL node set as entry point via 'Make entrypoint'
- HITL node has downstream nodes connected on at least one route
- Pipeline runnable in Chat interface

## Test Data

Pipeline input: any message

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Confirm in pipeline editor that HITL node shows the entry point indicator | Entry point indicator visible on HITL node |
| 2 | In Chat interface, trigger the pipeline run | Execution starts immediately from HITL; pipeline pauses for human decision |
| 3 | Verify USER MESSAGE is displayed | Configured USER MESSAGE appears with action buttons |
| 4 | Click Approve | Pipeline resumes and executes the downstream Approve route node; pipeline completes |

## Expected Final State

Pipeline resumes and executes the downstream Approve route node; pipeline completes

## Pass/Fail Criteria

**Pass:**
- Pipeline successfully starts from HITL as entry point
- First user action is always a human decision

**Fail:**
- Pipeline fails to start with HITL as entry point
- Entry point designation has no effect
