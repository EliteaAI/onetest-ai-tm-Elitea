---
id: ELITEA-3437
title: "Code-Node Pipeline Predict Latency Drops for LLM-Free Pipelines"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:python_sandbox, int:pyodide, nfr:performance, story:6717]
requirements: [EliteaAI/elitea_issues#6717]
---
# ELITEA-3437: Code-Node Pipeline Predict Latency Drops for LLM-Free Pipelines

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm the core fix for #6717 — a simple, LLM-free code-node pipeline no longer pays the ~65s stdin-timer leak, and per-phase sandbox timings are present in the predict response.

**Coverage:** Regression — `indexer_worker#129` (stdin timer leak, eager micropip removal), `elitea-sdk#649` (light preamble), `elitea_core#458` (budget-door skip).

## Preconditions

- Access to create/run a pipeline
- Available predict budget

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a pipeline with 3 `code` nodes chained in sequence (no `llm` node, no `decision:` edge, next-input suggestion off), each node doing trivial work, e.g. `result = {"node": "n1"}; print(result)`. | Pipeline saves successfully. |
| 2 | Run predict from the UI and note the elapsed time. | Predict completes in roughly 2-3 seconds, not ~60s+. |
| 3 | Run the same pipeline via REST/webhook predict. | Same fast completion; response is returned promptly, not after a ~30s+ stall. |
| 4 | Inspect the predict response/output JSON for per-node sandbox timing fields. | Fields `startup_ms`, `load_pyodide_ms`, `init_env_ms`, `install_imports_ms`, `user_code_ms`, `total_ms` are present and roughly sum to `total_ms`. |

## Expected Final State

The 3-code-node pipeline predicts in a few seconds (both UI and REST), and per-phase timing data is visible in the response.

## Pass/Fail Criteria

**Pass:**
- Steps 2-3 complete in the low single-digit seconds, not ~60s+
- Step 4's timing fields are present and internally consistent

**Fail:**
- Predict still takes ~30s or more (stdin-timer leak regressed)
- Timing fields are missing or clearly inconsistent (e.g. `total_ms` far smaller than the sum of phases)
