---
id: ELITEA-1770
title: "Multiple Code Nodes With debug:true — Each Saves Its Own Timestamped Artifact"
priority: high
type: functional
module: pipelines/code-node
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5203]
---
# ELITEA-1770: Multiple Code Nodes With `debug: true` — Each Saves Its Own Artifact

**Module:** Pipelines / Code Node · **Priority:** High · **Type:** Functional

**Objective:** Verify that when a pipeline has multiple code nodes each with `debug: true`, each node saves its own separate timestamped `.py` artifact to the `code-debug` bucket — artifacts are not merged or overwritten across nodes in the same run.

## Preconditions

- A pipeline has two or more code nodes (e.g., `node_a` and `node_b`)
- All code nodes have `debug: true` set

## Test Data

| Field | Value |
|-------|-------|
| Pipeline | Pipeline with at least two code nodes |
| Node names | e.g., `node_a`, `node_b` |
| Both `debug` flags | `true` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Set `debug: true` on both code nodes in the pipeline YAML; save | Pipeline saved |
| 2 | Run the pipeline | Both code nodes execute |
| 3 | Navigate to **Artifacts → `code-debug` bucket** | Two new `.py` files present |
| 4 | Verify filenames | One file prefixed `node_a__<timestamp>.py`, another `node_b__<timestamp>.py` |
| 5 | Open each file and verify content | Each file contains that node's own user code (not the other node's code) |
| 6 | Run the pipeline a second time | Two more timestamped artifacts added; previous artifacts not overwritten |

## Expected Final State

`code-debug` bucket contains one artifact per node per run, each named and scoped to its own node. No cross-node content mixing.

## Pass/Fail Criteria

**Pass:**
- Separate artifact per node with correct `<NodeName>__<timestamp>.py` filename
- Each artifact contains that node's own code only
- Re-run adds new timestamped files without overwriting previous ones

**Fail:**
- Only one artifact saved for both nodes
- Artifacts overwrite each other or contain mixed content
- Second run overwrites first run's artifacts
