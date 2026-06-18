---
id: ELITEA-0844
title: "Verify pipeline node renaming shows proper error messages on failure"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines]
requirements: []
---
# ELITEA-0844: Verify pipeline node renaming shows proper error messages on failure

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** When renaming pipeline nodes fails (e.g., duplicate names, invalid characters, empty names), the error messages display incorrectly or are not shown properly. This is a negative test complementing TC-0043 which covers the happy path of node renaming. This test verifies error handling for invalid rename operations.

## Preconditions

User logged into Elitea stage.elitea.ai
A pipeline exists with at least two nodes (e.g., two LLM nodes: 'LLM 1' and 'LLM 2')

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the pipeline detail page with multiple nodes | Pipeline editor loads showing at least two nodes (e.g., 'LLM 1' and 'LLM 2') |
| 2 | Double-click the name label of 'LLM 1' to enter rename mode | Node name becomes editable with an input field showing the current name |
| 3 | Clear the name field and try to confirm with Enter or clicking outside (empty name) | A clear, readable error message appears indicating that node name cannot be empty. The node retains its original name 'LLM 1' |
| 4 | Double-click the name label again and type the name of the other existing node (e.g., 'LLM 2') to create a duplicate name | A clear, readable error message appears indicating that a node with this name already exists. The node retains its original name |
| 5 | Verify the error message is displayed in a readable format (not raw JSON, not truncated, not overlapping UI elements) | Error message is displayed as a proper toast notification or inline message. Text is fully readable, properly formatted, and does not overlap with other UI elements |
| 6 | Try renaming the node with special characters that may be invalid (e.g., '/', '\', or excessively long names) | Appropriate error messages are shown for invalid characters or length violations. Messages are clear and actionable |
| 7 | After all error scenarios, verify the node still has its original name and functions correctly | Node retains original name 'LLM 1'. The pipeline flow, connections, and node configuration are unaffected by failed rename attempts |
| 8 | Successfully rename the node to a valid, unique name (e.g., 'My LLM Node') | Node is renamed successfully. No errors displayed. The node data-id updates to reflect the new name |
| 9 | After successful rename, verify that all connections (edges) to/from the renamed node are preserved and the pipeline remains valid | All edges connected to the renamed node are intact. Edge data-testids reflect the new node name. Pipeline can still be saved and executed |
| 10 | Rename the node back to its original name ('LLM 1') and verify this is allowed (roundtrip rename) | Node accepts the original name without duplicate error — the old name is free since the node currently holds a different name. Roundtrip rename works correctly |
| 11 | Save the pipeline after renaming, then refresh the page and verify the renamed node persists with its new name | After page refresh, the node retains its renamed value. Name is persisted to the backend and survives reload |
| 12 | Switch to YAML view and verify the renamed node name is correctly reflected in the YAML representation | YAML view shows the renamed node with the correct name. Node references in edges and configurations within the YAML match the new name |

## Expected Final State

YAML view shows the renamed node with the correct name. Node references in edges and configurations within the YAML match the new name

## Pass/Fail Criteria

PASS: Error messages for invalid rename operations are clear, properly formatted, visible, and the node retains its original name; successful rename preserves connections; roundtrip rename works; name persists after save/refresh; YAML view reflects the new name
FAIL: Error messages are improperly displayed (raw JSON, truncated, overlapping), missing, node left in inconsistent state, connections broken after rename, name lost on refresh, or YAML view shows stale name
