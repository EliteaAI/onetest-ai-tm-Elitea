---
id: ELITEA-0841
title: "Verify deprecated Pipeline node type does not cause errors when invoking nested pipelines"
priority: high
type: functional
module: pipelines
status: draft
execution_type: manual
tags: [feat:pipelines]
requirements: []
---
# ELITEA-0841: Verify deprecated Pipeline node type does not cause errors when invoking nested pipelines

**Module:** Pipelines · **Priority:** High · **Type:** Functional

**Objective:** The deprecated "Pipeline" node type throws errors when attempting to invoke nested pipelines. Users with existing pipelines that use the deprecated node type encounter runtime errors. This test verifies that deprecated Pipeline nodes are handled gracefully, either by migration to the current approach or clear error messaging.

## Preconditions

User logged into Elitea stage.elitea.ai
Knowledge of the deprecated Pipeline node type vs. current nested pipeline invocation method
A pipeline exists that uses the deprecated Pipeline node type to invoke a nested pipeline (or ability to import one)

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the pipeline creation page. Check the node type menu (click + button) for the presence of a 'Pipeline' node type | The deprecated 'Pipeline' node type should either be removed from the menu or clearly marked as deprecated. Available node types should guide users to the correct approach for nested pipelines |
| 2 | If a deprecated 'Pipeline' node type exists in the menu, add it to the canvas | If allowed, the node is added. A deprecation warning or migration notice should be displayed to the user |
| 3 | Open or import an existing pipeline that contains the deprecated Pipeline node type configured to invoke a nested pipeline | Pipeline loads. The deprecated Pipeline node is visible on the canvas, possibly with a visual indicator of its deprecated status |
| 4 | Attempt to execute the pipeline by sending a message in the embedded chat | One of: (a) Pipeline executes successfully with backward compatibility, (b) A clear, user-friendly error message explains the deprecated node and suggests migration steps, or (c) The node is auto-migrated to the current approach |
| 5 | If execution fails, check the error message for clarity and actionability | Error message clearly identifies the deprecated Pipeline node as the issue. Message includes guidance on how to migrate (e.g., 'Replace the deprecated Pipeline node with the current nested pipeline approach') |
| 6 | If the deprecated node exists, check its configuration panel for migration guidance or documentation links | Configuration panel shows deprecation notice with migration instructions or a link to documentation |
| 7 | Replace the deprecated Pipeline node with the current approach for nested pipeline invocation | The replacement node is configured successfully with the nested pipeline reference |
| 8 | Execute the pipeline with the migrated node | Pipeline executes successfully. The nested pipeline is invoked correctly without errors |

## Expected Final State

Pipeline executes successfully. The nested pipeline is invoked correctly without errors

## Pass/Fail Criteria

PASS: Deprecated Pipeline node either works with backward compatibility, shows clear migration guidance, or is automatically migrated. No cryptic errors
FAIL: Deprecated Pipeline node throws unhandled runtime errors without explanation, lacks migration guidance, or silently fails with no output
