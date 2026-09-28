---
id: ELITEA-3439
title: "Non-Stdlib Package Import Still Installs via the Lazy Micropip Path"
priority: medium
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipeline_nodes, feat:python_sandbox, int:pyodide, story:6717, regression]
requirements: [EliteaAI/elitea_issues#6717]
---
# ELITEA-3439: Non-Stdlib Package Import Still Installs via the Lazy Micropip Path

**Module:** Pipelines · **Priority:** Medium · **Type:** Functional

**Objective:** Confirm removing the eager `pyodide.loadPackage(["micropip"])` call (`indexer_worker#129`) did not break on-demand installation of a non-stdlib package inside a code node — this was left unverified in the PR's own test plan.

**Coverage:** Regression — `indexer_worker#129`.

## Preconditions

- Access to create/run a pipeline with a `code` node

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Create a single-code-node pipeline whose code imports a non-stdlib package, e.g. `import numpy as np; result = {"numpy_version": np.__version__, "mean": float(np.array([1, 2, 3]).mean())}; print(result)`. | Pipeline saves successfully. |
| 2 | Run predict. | The node completes successfully; the printed/returned result shows a valid `numpy_version` and correct computed value — no `ModuleNotFoundError` or install failure. |
| 3 | Inspect the predict response's per-phase timing fields. | `install_imports_ms` is present and non-zero for this node, confirming the package was installed via the lazy `install_imports` path rather than a pre-existing eager load. |
| 4 | Run the same pipeline a second time. | Still succeeds (confirms the lazy install path is reliably repeatable, not a one-off cold-cache fluke). |

## Expected Final State

A code node that imports a non-stdlib package installs and runs it correctly on every run, using the lazy install path introduced when the eager `micropip` load was removed.

## Pass/Fail Criteria

**Pass:**
- Steps 2 and 4 both succeed with correct output
- Step 3 shows a non-zero `install_imports_ms`

**Fail:**
- The import fails (`ModuleNotFoundError` or install timeout) on either run
