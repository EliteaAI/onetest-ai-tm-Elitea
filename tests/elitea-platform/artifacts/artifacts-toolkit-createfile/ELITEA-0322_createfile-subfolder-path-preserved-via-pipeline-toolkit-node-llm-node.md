---
id: ELITEA-0322
title: "createFile Subfolder Path Preserved via Pipeline (Toolkit Node + LLM Node)"
priority: high
type: functional
module: artifacts-toolkit-createfile
status: draft
execution_type: manual
tags: [feat:artifacts, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3690]
---
# ELITEA-0322: createFile Subfolder Path Preserved via Pipeline (Toolkit Node + LLM Node)

**Module:** Artifacts Toolkit Createfile · **Priority:** High · **Type:** Functional

**Objective:** Verify that `createFile` preserves the subfolder path when invoked from a Pipeline — both via a direct Toolkit node and via an LLM node that calls the tool through an Agent with the Artifact Toolkit.

**Coverage:**
- Pipeline Toolkit node with CreateFile configured with `filename=pipeline/toolkit_node.txt`
- Pipeline LLM node (Agent with Artifact Toolkit) invoking createFile at `pipeline/llm_node.txt`
- Both files appear at correct subfolder paths in the bucket after pipeline run
- Content verifiable for both files

## Preconditions

- Logged in to next.elitea.ai, Private project
- A Pipeline configured with:
  1. A Toolkit node using the Artifact Toolkit's CreateFile tool — filename = pipeline/toolkit_node.txt, filedata = toolkit node created
  2. An LLM node with an Agent (Artifact Toolkit attached) — instructed to create pipeline/llm_node.txt with content llm node created
- Artifacts bucket page open in a separate browser tab for visual verification

## Test Data

| Node type | Target filename | Filedata |
|---|---|---|
| Toolkit node | pipeline/toolkit_node.txt | toolkit node created |
| LLM node (Agent) | pipeline/llm_node.txt | llm node created |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Artifacts bucket in a separate browser tab (Artifacts menu → select the bucket). | Bucket file tree is visible and ready for checking. |
| 2 | Open the Pipeline. Confirm the Toolkit node is configured: Filename = pipeline/toolkit_node.txt, Filedata = toolkit node created. | Toolkit node shows the correct parameter values. |
| 3 | Confirm the LLM node Agent is configured to create pipeline/llm_node.txt with content llm node created. | Agent instruction references the correct subfolder path. |
| 4 | Run the pipeline. | Pipeline executes and completes with success status; no errors in run output. |
| 5 | Switch to the Artifacts bucket tab and refresh. Check for toolkit_node.txt. | toolkit_node.txt exists inside pipeline/. No toolkit_node.txt at the bucket root. |
| 6 | In the same bucket tab, check for llm_node.txt. | llm_node.txt exists inside pipeline/. No llm_node.txt at the bucket root. |
| 7 | Click on pipeline/toolkit_node.txt in the bucket UI to preview its content. | Content preview shows: toolkit node created. |
| 8 | Click on pipeline/llm_node.txt in the bucket UI to preview its content. | Content preview shows: llm node created. |

## Expected Final State

Content preview shows: llm node created.

## Pass/Fail Criteria

**Pass:**
- Pipeline run completes with no errors
- Both files (pipeline/toolkit_node.txt and pipeline/llm_node.txt) appear at their correct subfolder paths in the Artifacts bucket
- No files created at root with bare names
- Content preview for each file matches expected values

**Fail:**
- Pipeline run fails or errors out
- Either file appears at bucket root instead of pipeline/ subfolder
- Files missing from bucket after run
- Content preview shows wrong value
