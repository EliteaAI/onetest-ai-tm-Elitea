---
id: ELITEA-0849
title: "Verify Swarm Mode toggle is not available for pipelines"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines]
requirements: []
---
# ELITEA-0849: Verify Swarm Mode toggle is not available for pipelines

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Swarm Mode is an agent-only feature that should not be exposed in the pipeline configuration UI. When Swarm Mode is active for pipelines, it causes unintended behavior. This test verifies that pipeline configuration pages do not expose agent-only features like Swarm Mode.

## Preconditions

User logged into Elitea stage.elitea.ai
At least one pipeline exists or user can create a new pipeline

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines page (/app/pipelines/all) | Pipeline dashboard loads with list of pipelines |
| 2 | Click 'Create' to create a new pipeline or open an existing pipeline | Pipeline detail/create page loads with Configuration tab active |
| 3 | Inspect the GENERAL configuration panel on the left side for any Swarm Mode toggle or switch | Swarm Mode toggle is NOT present in the pipeline configuration panel |
| 4 | Expand the Toolkits section in the pipeline configuration | Toolkits section expands showing toolkit cards and available switches |
| 5 | Verify the available switches in the Toolkits section (Smart Tools Selection, Python sandbox, Data Analysis, Planner) | Only pipeline-appropriate switches are shown. Swarm Mode switch is NOT present |
| 6 | Check the pipeline YAML editor by clicking the 'Yaml' toggle button | YAML editor opens showing pipeline configuration without any swarm_mode settings |
| 7 | Search the YAML content for any 'swarm' related configuration keys | No swarm-related keys found in pipeline YAML configuration |
| 8 | Create a pipeline with nodes (e.g., LLM node) and save it. Re-open and verify no Swarm Mode appeared after save | Saved pipeline does not acquire Swarm Mode settings. Configuration remains pipeline-appropriate |

## Expected Final State

Saved pipeline does not acquire Swarm Mode settings. Configuration remains pipeline-appropriate

## Pass/Fail Criteria

PASS: Swarm Mode toggle is absent from pipeline configuration in both Flow and YAML views
FAIL: Swarm Mode toggle appears in pipeline configuration UI or YAML, or Swarm Mode settings are persisted in pipeline configuration
