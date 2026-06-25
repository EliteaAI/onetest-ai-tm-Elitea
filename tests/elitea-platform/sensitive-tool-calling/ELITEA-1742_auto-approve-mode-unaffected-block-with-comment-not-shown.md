---
id: ELITEA-1742
title: "Auto-Approve Mode Unaffected — Block with Comment Not Shown When Auto-Approve Is Active"
priority: high
type: functional
module: sensitive-tool-calling
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5318]
---
# ELITEA-1742: Auto-Approve Mode Unaffected — Block with Comment Not Shown When Auto-Approve Is Active

**Module:** Sensitive Tool Calling · **Priority:** High · **Type:** Functional

**Objective:** Verify that auto-approve (supported for pipeline code nodes and agents invoked via elitea_core APIs) is unaffected by the Block with Comment addition — the HITL dialog does not appear and the tool executes automatically in those contexts.

**Note:** Auto-approve is only supported for: (1) pipeline code nodes, and (2) agents invoked through elitea_core APIs. It is not available in standard agent chat.

## Preconditions

- A pipeline with a code node is configured, and the sensitive tool called from that code node has auto-approve enabled **OR** an agent is invoked via elitea_core API with auto-approve configured for the sensitive tool
- The sensitive tool under test is marked as sensitive in guardrails configuration

## Test Data

| Field | Value |
|-------|-------|
| Context | Pipeline code node (or elitea_core API invocation) with auto-approve enabled |
| Tool | Any tool marked as sensitive with auto-approve active |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Trigger the pipeline (or elitea_core API call) that invokes the auto-approved sensitive tool | Tool call dispatched |
| 2 | Observe for any HITL dialog appearance | NO authorization dialog appears — not Authorize / Block / Block with Comment |
| 3 | Observe execution result | Tool executes automatically; pipeline/API call completes normally |
| 4 | Verify the tool's side effect occurred | Side effect present (tool executed successfully without manual approval) |

## Expected Final State

Auto-approved tool executes without any HITL dialog in pipeline code node / elitea_core API context. Block with Comment does not interfere.

## Pass/Fail Criteria

**Pass:**
- No HITL dialog appears in the auto-approve context
- Tool executes automatically
- Execution completes normally

**Fail:**
- Block with Comment dialog unexpectedly appears in an auto-approve context
- Tool blocked despite auto-approve being configured
- Auto-approve behavior broken by #5318 changes
