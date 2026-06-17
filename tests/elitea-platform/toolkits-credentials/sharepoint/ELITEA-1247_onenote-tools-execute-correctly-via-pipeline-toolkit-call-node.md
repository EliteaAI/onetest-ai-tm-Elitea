---
id: ELITEA-1247
title: "OneNote tools execute correctly via Pipeline Toolkit Call node"
priority: high
type: functional
module: sharepoint
status: ready
execution_type: manual
tags: [feat:toolkits, issue:2355, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#2355]
---
# ELITEA-1247: OneNote tools execute correctly via Pipeline Toolkit Call node

**Module:** Sharepoint · **Priority:** High · **Type:** Functional

**Objective:** Verify that OneNote toolkit tools (onenote_get_notebooks, onenote_read_page, index_data) execute correctly when called from a Pipeline Toolkit Call node and that output is correctly passed to a downstream LLM node.

**Coverage:**
- Toolkit Call node with onenote_get_notebooks → LLM node
- Toolkit Call node with onenote_read_page → LLM node
- Toolkit Call node with index_data (Include Onenote) within pipeline context

## Preconditions

- SharePoint toolkit with Delegated OAuth auth configured in the project
- A Pipeline exists (or is created) with a Toolkit Call node configured with the SharePoint toolkit
- A valid OneNote page ID is available

## Test Data

- Toolkit Call node 1: onenote_get_notebooks (no params)
- Toolkit Call node 2: onenote_read_page (valid page ID, capture_images=False)
- Toolkit Call node 3: index_data (Include Onenote checked, filter {})

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open a Pipeline. Add a Toolkit Call node with the SharePoint toolkit, tool set to onenote_get_notebooks. Connect it to an LLM node. Run the pipeline. | Toolkit node returns notebooks list; LLM node produces a summary response from the output. No errors. |
| 2 | Reconfigure the Toolkit Call node with onenote_read_page (valid page ID, capture_images=False). Run the pipeline. | Page content returned by toolkit node; LLM node processes the plain text content correctly. |
| 3 | Reconfigure the Toolkit Call node with index_data (Include Onenote checked, Onenote Filter {}). Run the pipeline. | Indexing executes successfully within the pipeline context; completion confirmed without errors. |

## Expected Final State

Indexing executes successfully within the pipeline context; completion confirmed without errors.

## Pass/Fail Criteria

**Pass:**
- All OneNote toolkit tools execute correctly from Pipeline Toolkit Call node
- Output passed to downstream LLM node in all cases

**Fail:**
- Toolkit Call node errors in pipeline context; output not passed downstream
