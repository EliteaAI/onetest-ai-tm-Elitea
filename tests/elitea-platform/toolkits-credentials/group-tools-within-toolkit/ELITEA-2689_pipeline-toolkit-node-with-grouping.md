---
id: ELITEA-2689
title: "Pipeline Toolkit Node Shows Correct (Chosen) Tool"
priority: high
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, pipelines, integration]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2689: Pipeline Toolkit Node Shows Correct (Chosen) Tool

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** High · **Type:** Functional

**Objective:** Verify pipeline LLM nodes with attached toolkits display tool information correctly after grouping changes.

**Coverage:**
- Pipeline toolkit node displays tools correctly
- Tool count matches the source toolkit configuration
- Pipeline execution works correctly with grouped toolkit
- No regression in pipeline-toolkit integration

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- A pipeline with a toolkit node exists
- The toolkit has tools from multiple groups selected
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the toolkit used in the pipeline and note which tools are selected and their counts. | Tool selection state is documented. |
| 2 | Navigate to Pipelines page and open the pipeline with a toolkit node. | Pipeline editor opens. |
| 3 | Click on the LLM node that has the toolkit attached. | Node configuration panel opens. |
| 4 | Verify the toolkit entry shows tools section. | Tools section is visible in the node configuration. |
| 5 | Verify shown tools matches the toolkit configuration. | Shown Tools are thouse selected in te source toolkit. |
| 6 | Execute the pipeline. | Pipeline execution **starts**. |
| 7 | Verify pipeline execution completes successfully. | Execution **completes** without errors. |
| 8 | Verify toolkit tools are available during execution and results are correct. | Tool execution results are **correct**. |

## Expected Final State

Pipeline executes successfully with correct toolkit tool integration.

## Pass/Fail Criteria

**Pass:**
- Pipeline toolkit node displays tools correctly
- Tools matche the source toolkit configuration
- Pipeline execution works correctly with grouped toolkit
- No regression in pipeline-toolkit integration

**Fail:**
- Pipeline toolkit node displays incorrect tool information
- Tool does not match the source toolkit
- Pipeline execution fails due to toolkit changes
- Tool results are incorrect during pipeline execution
