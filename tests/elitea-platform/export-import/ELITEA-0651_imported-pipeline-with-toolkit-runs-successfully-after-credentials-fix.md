---
id: ELITEA-0651
title: "Imported Pipeline with Toolkit Runs Successfully After Credentials Fix"
priority: high
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3824]
---
# ELITEA-0651: Imported Pipeline with Toolkit Runs Successfully After Credentials Fix

**Module:** Export Import · **Priority:** High · **Type:** Functional

**Objective:** Verify that an imported pipeline with an attached toolkit runs successfully end-to-end after toolkit credentials are configured.

**Coverage:**
- Toolkit credentials can be updated on an imported pipeline
- Pipeline run completes successfully (Toolkit node + LLM node)
- Toolkit node invokes the configured tool and returns a result
- LLM node produces a response based on toolkit output

**Prerequisite:** TC-0705 must pass first (YAML is clean, toolkit is attached).

## Preconditions

- TC-0705 has passed: pipeline has been imported, `toolkits:` section is absent from YAML, and toolkit is confirmed attached
- Logged in to {{base_url}} as Owner/Editor
- Valid credentials available for the attached toolkit (e.g., GitHub personal access token)

## Test Data

- Imported pipeline: result of TC-0705 import (e.g., PipelineWithToolkit_Export — imported copy)
- Toolkit: GitHub toolkit
- Toolkit node tool: e.g., get_file_contents
- LLM node prompt: e.g., "Summarize the result from the toolkit above"
- Credentials: valid GitHub personal access token with repo read access

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the imported pipeline's Toolkits panel. Open the attached toolkit settings and enter / fix the credentials (API token, auth). Save. | Toolkit credentials saved successfully; no error. |
| 2 | Open the imported pipeline and click Run. | Pipeline execution starts; run enters In Progress state. |
| 3 | Wait for the run to complete. Inspect the run output: check the Toolkit node output and LLM node output. | Run completes with Success status. Toolkit node executed the configured tool and returned a result. LLM node produced a response based on toolkit output. No errors in run log. |

## Expected Final State

Run completes with Success status. Toolkit node executed the configured tool and returned a result. LLM node produced a response based on toolkit output. No errors in run log.

## Pass/Fail Criteria

**Pass:**
- Toolkit credentials saved without error (step 1)
- Pipeline run completes with Success status (step 3)
- Toolkit node returned a result (step 3)
- LLM node produced a response (step 3)

**Fail:**
- Credentials cannot be saved on the imported pipeline's toolkit
- Pipeline run fails with a toolkit-related error (not a credential issue)
- Toolkit node produces no output or an unexpected error
