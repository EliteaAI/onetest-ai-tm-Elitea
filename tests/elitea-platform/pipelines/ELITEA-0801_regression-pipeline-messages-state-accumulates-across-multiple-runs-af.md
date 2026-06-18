---
id: ELITEA-0801
title: "Regression — Pipeline Messages State Accumulates Across Multiple Runs After Sub-Participant Change"
priority: high
type: functional
module: pipelines
status: ready
execution_type: manual
tags: [feat:pipelines, feat:agents, regression, r-2.0.3]
requirements: [EliteaAI/elitea_issues#4790]
---
# ELITEA-0801: Regression — Pipeline Messages State Accumulates Across Multiple Runs After Sub-Participant Change

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** Regression — verify that the Pipeline messages state correctly accumulates entries across multiple runs after the sub-participant `chat_history` exclusion change. Each run should add a new entry to the messages state, and previous run entries must not be discarded.

**Coverage:**
- Pipeline messages state is populated after run 1
- Pipeline messages state contains entries from both run 1 and run 2 after run 2 completes
- Previous run history is not wiped by the sub-participant change
- Messages state grows incrementally with each run

## Preconditions

- Logged in to {{base_url}}
- A pipeline is configured and runnable
- Enhancement EliteaAI/elitea_issues#4790 is deployed

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the pipeline from the Pipelines page and run it with a sample input. After completion, inspect the messages state. | Run 1 completes successfully. Messages state contains an entry for run 1. |
| 2 | Run the same pipeline a second time (same or different input). After completion, inspect the messages state again. | Messages state contains entries for both run 1 and run 2. Previous run history is preserved and not overwritten or discarded. |

## Expected Final State

Messages state contains entries for both run 1 and run 2. Previous run history is preserved and not overwritten or discarded.

## Pass/Fail Criteria

**Pass:**
- After run 2, messages state contains entries from both run 1 and run 2

**Fail:**
- Messages state after run 2 contains only run 2 (prior history discarded)
- Messages state is empty after runs
- Pipeline errors during execution
