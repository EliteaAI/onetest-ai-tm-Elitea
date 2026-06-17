---
id: ELITEA-0652
title: "Imported Parent + Child Pipelines with Mixed Toolkits Run Successfully After Credentials Fix"
priority: high
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3824]
---
# ELITEA-0652: Imported Parent + Child Pipelines with Mixed Toolkits Run Successfully After Credentials Fix

**Module:** Export Import · **Priority:** High · **Type:** Functional

**Objective:** Verify that an imported parent pipeline (GitHub toolkit) and child pipeline (MCP toolkit) run successfully as a chain after credentials are configured on both.

**Coverage:**
- GitHub toolkit credentials can be configured on the imported parent pipeline
- MCP toolkit credentials/config can be set on the imported child pipeline
- Full pipeline chain (parent → child) runs successfully
- Both Toolkit nodes produce results; LLM node in child produces a response

**Prerequisite:** TC-0704 must pass first (YAML is clean on both, toolkits are attached).

## Preconditions

- TC-0704 has passed: both pipelines imported, neither YAML contains `toolkits:`, both toolkits confirmed attached
- Logged in to {{base_url}} as Owner/Editor
- Valid credentials available for GitHub toolkit (parent) and MCP toolkit (child)

## Test Data

Pipeline: Imported parent | Toolkit: GitHub toolkit | Tool: e.g., get_file_contents
Pipeline: Imported child | Toolkit: MCP toolkit | Tool: any MCP tool
Credentials: valid GitHub PAT (parent), valid MCP server config (child)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | On the imported parent pipeline, open the GitHub toolkit settings and enter / fix the credentials. Save. | GitHub toolkit credentials saved on parent pipeline without error. |
| 2 | On the imported child pipeline, open the MCP toolkit settings and enter / fix the credentials/config. Save. | MCP toolkit credentials saved on child pipeline without error. |
| 3 | Open the imported parent pipeline and click Run. Wait for the full chain to complete. | Both parent and child runs complete with Success status. No toolkit-related errors in either run. |
| 4 | Inspect the Toolkit node output in both pipelines' run logs. | Parent: GitHub toolkit node returned a result. Child: MCP toolkit node returned a result. LLM node in child produced a response. |

## Expected Final State

Parent: GitHub toolkit node returned a result. Child: MCP toolkit node returned a result. LLM node in child produced a response.

## Pass/Fail Criteria

**Pass:**
- Credentials saved on both imported pipelines without error (steps 1–2)
- Full pipeline chain completes with Success status (step 3)
- GitHub toolkit node returned a result (step 4)
- MCP toolkit node returned a result (step 4)
- LLM node in child produced a response (step 4)

**Fail:**
- Credentials cannot be saved on either imported pipeline's toolkit
- Pipeline chain fails due to toolkit not being attached (not a credential issue)
- Either Toolkit node produces no output or an unexpected error
