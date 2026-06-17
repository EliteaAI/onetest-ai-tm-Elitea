---
id: ELITEA-0667
title: "Exported pipeline MD includes pipeline_settings for pipeline nodes"
priority: medium
type: functional
module: export-import
status: ready
execution_type: manual
tags: [feat:pipelines, R-2.0.1, eng:ui, bug]
requirements: [ProjectAlita/projectalita.github.io#3711]
---
# ELITEA-0667: Exported pipeline MD includes pipeline_settings for pipeline nodes

**Module:** Export Import · **Priority:** Medium · **Type:** Functional

**Objective:** Objective
Verify that exporting a pipeline containing nodes generates a Markdown (.md) file that includes pipeline_settings entries for those nodes. The exported configuration must contain layout attributes such as width and height, ensuring the pipeline layout can be preserved during import.

Coverage
- Exported MD file contains a top-level or pipeline-scoped pipeline_settings object.
- Each node includes pipeline_settings with width and height properties.
- Exported values match the values configured in the pipeline editor.

## Preconditions

- Logged in to {{base_url}} as a user with pipelines.create and pipelines.export permissions.
- At least one pipeline with multiple nodes exists.

## Test Data

- Environment URL: {{base_url}}
- Example Pipeline URL: {{base_url}}

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to any pipeline containing multiple nodes with configured mappings. (Example: open ImportToolkitTestingPipeline). | Pipeline canvas loads successfully. |
| 2 | Click Menu → Export → Export pipeline. | The pipeline is successfully exported. A Markdown (.md) file is downloaded locally. |
| 3 | Open the exported .md file using a text editor (VS Code, Notepad++, etc.) and search for the term:  pipeline_settings | - A pipeline_settings object is present in the exported file. - The object appears within node configuration. |
| 4 | Inspect the pipeline_settings section in the exported file. | The object contains both for each node: - width - height  The values correspond to the node dimensions configured in the pipeline UI.  Example pipeline_settings:   edges:   - id: xy-edge__Toolkit 1---LLM 1     data: {}     type: custom     source: Toolkit 1     target: LLM 1   - id: xy-edge__LLM 1---Toolkit 2     data: {}     type: custom     source: LLM 1     target: Toolkit 2   - id: xy-edge__Toolkit 2---LLM 2     data: {}     type: custom     source: Toolkit 2     target: LLM 2   - id: xy-edge__LLM 2---LLM 3     data: {}     type: custom     source: LLM 2     target: LLM 3   - id: xy-edge__LLM 3---AlitaPipelineEnd     type: custom     source: LLM 3     target: END   nodes:   - id: END     data:       label: End     type: END     measured:       width: 460       height: 60     position:       x: 60       y: 5666   - id: Toolkit 1     data:       label: Toolkit 1     type: toolkit     measured:       width: 460       height: 1181     position:       x: 60       y: 60   - id: LLM 1     data:       label: LLM 1     type: llm     measured:       width: 460       height: 632     position:       x: 60       y: 1491   - id: Toolkit 2     data:       label: Toolkit 2     type: toolkit     measured:       width: 460       height: 1181     position:       x: 60       y: 2373   - id: LLM 2     data:       label: LLM 2     type: llm     measured:       width: 460       height: 730     position:       x: 60       y: 3804   - id: LLM 3     data:       label: LLM 3     type: llm     measured:       width: 460       height: 632     position:       x: 60       y: 4784   orientation: vertical   layout_version: '1.0' --- |

## Expected Final State

The object contains both for each node: - width - height  The values correspond to the node dimensions configured in the pipeline UI.  Example pipeline_settings:   edges:   - id: xy-edge__Toolkit 1---LLM 1     data: {}     type: custom     source: Toolkit 1     target: LLM 1   - id: xy-edge__LLM 1---Toolkit 2     data: {}     type: custom     source: LLM 1     target: Toolkit 2   - id: xy-edge__Toolkit 2---LLM 2     data: {}     type: custom     source: Toolkit 2     target: LLM 2   - id: xy-edge__LLM 2---LLM 3     data: {}     type: custom     source: LLM 2     target: LLM 3   - id: xy-edge__LLM 3---AlitaPipelineEnd     type: custom     source: LLM 3     target: END   nodes:   - id: END     data:       label: End     type: END     measured:       width: 460       height: 60     position:       x: 60       y: 5666   - id: Toolkit 1     data:       label: Toolkit 1     type: toolkit     measured:       width: 460       height: 1181     position:       x: 60       y: 60   - id: LLM 1     data:       label: LLM 1     type: llm     measured:       width: 460       height: 632     position:       x: 60       y: 1491   - id: Toolkit 2     data:       label: Toolkit 2     type: toolkit     measured:       width: 460       height: 1181     position:       x: 60       y: 2373   - id: LLM 2     data:       label: LLM 2     type: llm     measured:       width: 460       height: 730     position:       x: 60       y: 3804   - id: LLM 3     data:       label: LLM 3     type: llm     measured:       width: 460       height: 632     position:       x: 60       y: 4784   orientation: vertical   layout_version: '1.0' ---

## Pass/Fail Criteria

Pass
- Exported .md file contains pipeline_settings objects.
- Each relevant node includes width and height values.
- Values match the layout configured in the pipeline UI.

Fail
- pipeline_settings is missing from the exported file.
- width or height properties are missing.
- Exported values are incorrect or default values instead of configured ones.
