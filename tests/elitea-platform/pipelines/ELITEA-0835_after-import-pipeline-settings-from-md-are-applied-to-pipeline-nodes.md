---
id: ELITEA-0835
title: "After import, pipeline_settings from MD are applied to pipeline nodes"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [feat:import-forking, feat:pipelines, R-2.0.1, eng:ui, bug]
requirements: [ProjectAlita/projectalita.github.io#3711]
---
# ELITEA-0835: After import, pipeline_settings from MD are applied to pipeline nodes

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Objective
- Verify that importing a pipeline from a Markdown (.md) file correctly applies pipeline_settings for pipeline nodes so that the node layout and sizes are preserved immediately after import.
- The imported pipeline should render nodes using the sizes defined in the exported configuration, without requiring the user to manually save the pipeline.

Coverage
- Pipeline imported from an exported MD file preserves node pipeline_settings.
- Imported nodes render with the same width and height defined in the file.
- Node layout is applied immediately after import.
- Nodes do not overlap due to incorrect default sizes.

## Preconditions

- Logged in to
{{base_url}}
- User has permissions to perform pipeline creation and importing
- An exported pipeline MD file containing pipeline_settings is available (can be generated using TC-0515).

## Test Data

- Environment URL:
{{base_url}}
- Import file:
Exported pipeline .md file containing node pipeline_settings.
- Example pipeline file:
ImportToolkitTestingPipeline.md

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Pipelines page in the application. | Pipelines page loads successfully. |
| 2 | Click Import pipeline. | Import dialog appears allowing file upload. |
| 3 | Upload the exported pipeline .md file containing pipeline_settings. | The pipeline is successfully imported and opened in the pipeline editor. |
| 4 | Observe the pipeline canvas immediately after import (without making changes or saving). | Nodes render using the layout defined in the imported configuration. Nodes appear at their configured sizes and positions. |
| 5 | Verify that nodes on the canvas do not overlap due to incorrect default sizing. | Nodes are displayed correctly and the layout matches the configuration defined in the file. |

## Expected Final State

Nodes are displayed correctly and the layout matches the configuration defined in the file.

## Pass/Fail Criteria

Pass
- Imported pipeline nodes render using sizes defined in pipeline_settings.
- Nodes do not overlap after import.

Fail
- Nodes render using default sizes instead of imported configuration.
- Nodes overlap due to incorrect layout.
