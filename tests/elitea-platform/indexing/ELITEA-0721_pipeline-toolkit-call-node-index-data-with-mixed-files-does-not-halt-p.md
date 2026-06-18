---
id: ELITEA-0721
title: "Pipeline Toolkit Call Node: index_data With Mixed Files Does Not Halt Pipeline Execution"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:3672, r-2.0.2]
requirements: [ProjectAlita/projectalita.github.io#3672]
---
# ELITEA-0721: Pipeline Toolkit Call Node: index_data With Mixed Files Does Not Halt Pipeline Execution

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that a Pipeline with a Toolkit Call node running `index_data` on a mixed-file bucket executes to completion — the pipeline does not stop at the `index_data` step due to skipped files.

**Coverage:**
- Toolkit Call (`index_data`) node completes without "Tool execution failed"
- Pipeline continues to the downstream LLM node after `index_data`
- Both nodes present in Run Details with no fatal errors

## Preconditions

- Logged in to {{base_url}}
- Pipeline `skip-test-pipeline` configured: Toolkit Call node (`index_data`, `mixed-files-test`, suffix `pipe-skip-test`) → LLM node

## Test Data

- Pipeline: `skip-test-pipeline`
- Bucket: `mixed-files-test` (5 valid + 3 problematic files)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open `skip-test-pipeline`. Verify the Toolkit Call node is configured with `index_data` on `mixed-files-test`. | Configuration correct. Toolkit Call → LLM node chain set up. |
| 2 | Run the pipeline via the Chat interface. | Pipeline execution begins. Run chipset shows 🔄 In Progress. |
| 3 | Observe the Toolkit Call node chipset during the run. | Chipset does NOT show ❌ "Tool execution failed" due to skipped files. |
| 4 | Wait for pipeline completion. Check the run chipset final state. | Pipeline reaches a completed terminal state — not halted at the `index_data` step. |
| 5 | Open Run Details for the completed run. Check both node entries. | Both Toolkit Call and LLM nodes appear in Run Details with no fatal errors. |

## Expected Final State

Both Toolkit Call and LLM nodes appear in Run Details with no fatal errors.

## Pass/Fail Criteria

**Pass:**
- Toolkit Call node completes without "Tool execution failed"
- Pipeline reaches completion
- Both nodes present in Run Details with no fatal errors

**Fail:**
- Toolkit Call node fails due to skipped files, stopping the pipeline
- LLM node never executes
- Run Details shows termination at `index_data`
