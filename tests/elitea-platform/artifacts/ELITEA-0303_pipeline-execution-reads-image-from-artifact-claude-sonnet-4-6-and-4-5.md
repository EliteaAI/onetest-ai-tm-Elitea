---
id: ELITEA-0303
title: "Pipeline Execution Reads Image from Artifact – Claude Sonnet 4.6 and 4.5"
priority: critical
type: functional
module: artifacts
status: ready
execution_type: manual
tags: [feat:artifacts, eng:api, r-2.0.1, bug]
requirements: [ProjectAlita/projectalita.github.io#3644]
---
# ELITEA-0303: Pipeline Execution Reads Image from Artifact – Claude Sonnet 4.6 and 4.5

**Module:** Artifacts · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that a Pipeline node performing a readFile action on an image artifact completes successfully with both Claude Sonnet 4.6 and Claude Sonnet 4.5 as the executing LLM.

**Coverage:**
- Pipeline with Artifact Toolkit node reads an image successfully using Claude Sonnet 4.6
- Pipeline with Artifact Toolkit node reads an image successfully using Claude Sonnet 4.5
- No InternalSDKError or litellm errors are raised in either run

## Preconditions

- Logged in to {{base_url}}
- A Pipeline exists (or can be created) with at least one node using the Artifact Toolkit to read an image file
- The bucket contains at least one image file
- Pipeline's LLM is configurable and Claude Sonnet 4.6 and 4.5 are available

## Test Data

- Pipeline: any pipeline with Artifact Toolkit node using readFile on an image
- Image filename: sample.png
- LLM pass 1: Claude Sonnet 4.6
- LLM pass 2: Claude Sonnet 4.5

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Pipelines from the sidebar. | Pipelines list page is displayed. |
| 2 | Open an existing pipeline or create a new one with a node that reads an image from an artifact bucket. | Pipeline editor is accessible with the artifact-reading node configured. |
| 3 | Set the LLM to Claude Sonnet 4.6 and run the pipeline. | Pipeline execution starts. |
| 4 | Wait for the pipeline to finish and inspect the output. | Pipeline completes successfully. Image description is present in the output. No InternalSDKError is raised. |
| 5 | Switch the LLM to Claude Sonnet 4.5 and re-run the pipeline. | Pipeline execution starts with Claude Sonnet 4.5. |
| 6 | Wait for completion and inspect the output. | Pipeline completes successfully. Image description is present. No litellm errors or 500 InternalSDKError is raised. |

## Expected Final State

Pipeline completes successfully. Image description is present. No litellm errors or 500 InternalSDKError is raised.

## Pass/Fail Criteria

**Pass:**
- Pipeline completes execution and outputs image description for both Claude 4.6 and 4.5
- No API errors or internal SDK errors in either run

**Fail:**
- Pipeline fails with InternalSDKError (400 or 500) for either Claude version
- 'thinking' tag mismatch or litellm base64 error appears in pipeline output or logs
