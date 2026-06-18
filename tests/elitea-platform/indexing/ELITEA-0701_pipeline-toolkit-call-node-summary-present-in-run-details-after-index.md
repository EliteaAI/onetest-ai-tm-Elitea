---
id: ELITEA-0701
title: "Pipeline Toolkit Call Node — Summary Present in Run Details After index_data Executes"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0701: Pipeline Toolkit Call Node — Summary Present in Run Details After index_data Executes

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that a Pipeline's Toolkit Call node running index_data on a mixed-file source produces the summary in Run Details, and the pipeline continues to downstream nodes.

**Coverage:**
- Pipeline run completes without halting at the index_data Toolkit Call node
- Run Details for the node contains the structured summary (✅/⚠️/❌ sections with file names)
- Downstream node executes after index_data — pipeline not blocked by skipped files

## Preconditions

- Logged in to {{base_url}} a Pipeline with a Toolkit Call node configured with index_data and a downstream node (e.g., Printer or LLM node)
- Source bucket contains a mix of valid and skipped/failed files

## Test Data

- Pipeline: any pipeline with Toolkit Call (index_data) node + downstream node
- Collection suffix: pipe01; bucket: summary-mix-test

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline → verify Toolkit Call node is configured with index_data and collection suffix pipe01. | Configuration correct. |
| 2 | Click Run on the pipeline. | Execution starts. |
| 3 | Wait for the pipeline run to reach a terminal state. | Run completes. |
| 4 | Click Run Details → locate the Toolkit Call (index_data) node step. | Node step is listed. |
| 5 | Click the node step to inspect its output. | Output panel opens. |
| 6 | Verify the output contains the structured summary with ✅/⚠️/❌ sections and file names. | Summary present. |
| 7 | Verify the downstream node also completed execution. | Downstream node output is present in Run Details. |

## Expected Final State

Downstream node output is present in Run Details.

## Pass/Fail Criteria

**Pass:**
- Toolkit Call node output contains the full structured summary
- Pipeline continued to and completed the downstream node

**Fail:**
- Toolkit Call node output is empty or contains only a raw count
- Pipeline halted at the index_data step due to skipped files
