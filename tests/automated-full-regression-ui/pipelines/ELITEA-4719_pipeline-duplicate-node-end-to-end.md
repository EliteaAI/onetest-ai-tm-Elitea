---
id: ELITEA-4719
title: "Pipeline — Duplicate Node End-to-End"
priority: medium
type: functional
module: pipelines
status: ready
execution_type: automated
automation_test_id:
  - tests.ui.pipelines.test_pipeline_duplicate_node.test_pipeline_duplicate_node_end_to_end
automation_pr: https://github.com/EliteaAI/elitea-testing-public/commit/7d3b2c59000857140c8d2a60bbf9e8e14640afed
tags: [automated:UI:regression, feat:pipelines, epic:7093]
requirements: [EliteaAI/elitea_issues#7161, EliteaAI/elitea_issues#7418]
---

# ELITEA-4719: Pipeline — Duplicate Node End-to-End

**Module:** pipelines · **Priority:** medium · **Type:** functional

**Objective:** Verify the main Duplicate node flow: the copy is created with the same type and configuration, is disconnected and not the entry point, reuses the same tool attachment, follows the `_copy` / `_copy_2` naming, is removed by Discard, and executes correctly (with correct run highlighting) when wired in as the entry point.

---

## Preconditions

- User is logged in to the Elitea platform with Editor (or higher) role.
- An MCP is available in the project (e.g. "test-github-mcp") with at least one tool that needs no required input or uses fixed values (e.g. `get_me`).
- A saved pipeline exists: "MCP 1" (MCP, entry point, MCP + tool selected) → "LLM 1" (LLM) → End.

---

## Test Data

| Field | Value |
|-------|-------|
| Node to duplicate | MCP 1 |
| Run message | `go` |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the pipeline; click "MCP 1"; click the Duplicate icon in the panel footer | Toast: "MCP 1 duplicated as MCP 1_copy". A new card "MCP 1_copy" appears and its panel opens. "Save" is enabled |
| 2 | Inspect the "MCP 1_copy" panel (Flow) | Same MCP, Tool and input mapping values as "MCP 1" |
| 3 | Inspect the canvas | "MCP 1_copy" has no incoming and no outgoing edges and does NOT show the "Entrypoint" badge; "MCP 1" keeps its edges and badge |
| 4 | Inspect the TOOLS section (left side panel) | Only ONE entry for the MCP, "Used by: MCP 1, MCP 1_copy" |
| 5 | Click "MCP 1"; click Duplicate again | Toast: "MCP 1 duplicated as MCP 1_copy_2"; card "MCP 1_copy_2" is added |
| 6 | Click "Discard" | "MCP 1_copy" and "MCP 1_copy_2" are removed; canvas returns to the saved state |
| 7 | Duplicate "MCP 1" again; on "MCP 1_copy" click "Make Entrypoint"; connect "MCP 1_copy" Output → "LLM 1"; click "Save" | Pipeline saves; "MCP 1_copy" is the entry point |
| 8 | Click "Test Pipeline"; send `go` | During the run the "MCP 1_copy" card is highlighted as running (not "MCP 1"). Thinking steps show the tool call attributed to "MCP 1_copy" (e.g. "test-github-mcp: get_me (MCP 1_copy)"). The run completes |

---

## Expected Final State

Duplicating creates a disconnected, non-entry-point copy with identical configuration that shares the tool attachment; naming increments correctly; Discard removes unsaved copies; a wired-in copy runs and is highlighted correctly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Toast texts, naming, copied configuration, cleared connections/entry point and single attachment are as described.
- The copy is the highlighted node during its run.

**Fail:**
- Configuration differs, connections or the entry point are copied, a second attachment is created, or naming is wrong.
- Discard does not remove the copy.
- The original node is highlighted while the copy runs.

**Notes:** Copy placement (half overlap with the original) is accepted and not asserted. Full per-type duplicate coverage (all 10 node types, YAML diff) is in the manual suite.
