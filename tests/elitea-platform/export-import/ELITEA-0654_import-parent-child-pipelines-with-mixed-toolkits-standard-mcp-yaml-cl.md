---
id: ELITEA-0654
title: "Import Parent + Child Pipelines with Mixed Toolkits (Standard + MCP): YAML Clean, Toolkits Attached"
priority: high
type: functional
module: export-import
status: draft
execution_type: manual
tags: [feat:import-forking, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3824]
---
# ELITEA-0654: Import Parent + Child Pipelines with Mixed Toolkits (Standard + MCP): YAML Clean, Toolkits Attached

**Module:** Export Import · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a parent pipeline (GitHub toolkit) and a child pipeline (MCP toolkit) are imported, neither imported YAML retains a `toolkits:` section, and both toolkits are correctly attached.

**Coverage:**
- Parent pipeline with standard toolkit (GitHub) — imported YAML has no `toolkits:` section
- Child pipeline with MCP toolkit — imported YAML has no `toolkits:` section
- Both toolkits correctly attached after import
- Covers both standard and MCP toolkit types in one import scenario

**Note:** Functional run verification is covered separately in TC-0732.

## Preconditions

- Logged in to {{base_url}} as Owner/Editor
- Parent pipeline exists with GitHub toolkit attached, containing a Toolkit node and a child pipeline call
- Child pipeline exists with an MCP toolkit attached, containing a Toolkit node and an LLM node
- Both pipelines exported as .yaml files

## Test Data

Pipeline: Parent | Toolkit: GitHub toolkit | Tool: e.g., get_file_contents | Nodes: Toolkit node + child call
Pipeline: Child | Toolkit: MCP toolkit | Tool: any MCP tool | Nodes: Toolkit node + LLM node
Import files: parent_pipeline_export.yaml, child_pipeline_export.yaml

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open both export files in a text editor. Search for `toolkits:` in each. | Baseline: Both export files contain a `toolkits:` section. |
| 2 | Navigate to Pipelines → Import. Import the child pipeline export file. | Import completes without error; child pipeline appears in the list. |
| 3 | Navigate to Pipelines → Import. Import the parent pipeline export file. | Import completes without error; parent pipeline appears in the list. |
| 4 | Open the imported parent pipeline YAML view. Search for `toolkits:`. Then open its Toolkits panel. | YAML has no `toolkits:` section. GitHub toolkit is listed and attached. |
| 5 | Open the imported child pipeline YAML view. Search for `toolkits:`. Then open its Toolkits panel. | YAML has no `toolkits:` section. MCP toolkit is listed and attached. |

## Expected Final State

YAML has no `toolkits:` section. MCP toolkit is listed and attached.

## Pass/Fail Criteria

**Pass:**
- Both export files confirm `toolkits:` presence (baseline step 1)
- Neither imported pipeline YAML contains `toolkits:` section (steps 4–5)
- Both toolkits are correctly attached (steps 4–5)

**Fail:**
- Either imported YAML retains `toolkits:` section
- Toolkit missing from either imported pipeline
