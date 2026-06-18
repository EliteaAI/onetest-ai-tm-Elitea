---
id: ELITEA-0703
title: "Agent Chat — Summary Appears in index_data Tool Chipset Output"
priority: high
type: functional
module: indexing
status: draft
execution_type: manual
tags: [feat:indexer, story:4065, r-2.0.2]
requirements: [EliteaAI/elitea_issues#4065]
---
# ELITEA-0703: Agent Chat — Summary Appears in index_data Tool Chipset Output

**Module:** Indexing · **Priority:** High · **Type:** Functional

**Objective:** Verify that when an Agent invokes index_data via Chat on a mixed-file source, the tool chipset output includes the summary report and the chipset does not show a failure state.

**Coverage:**
- index_data tool chipset reaches a completed state — not "Tool execution failed"
- Chipset output contains the structured summary (✅/⚠️/❌ sections with file names)
- Agent's final response is present after the tool call completes

## Preconditions

- Logged in to {{base_url}} Agent created with an Artifacts toolkit attached and index_data enabled
- Bucket summary-mix-test contains a mix of valid and skipped/failed files (3 .txt + 1 empty PDF + 1 corrupted .docx)

## Test Data

- Agent name: any agent with Artifacts toolkit attached
- Prompt: "Please index all files in the summary-mix-test bucket using collection suffix agent01"
- Expected ✅ count: 3; expected ⚠️: 1; expected ❌: 1

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat → start a new conversation → add the agent as a participant. | Agent is available in the conversation. |
| 2 | Send the prompt: 'Please index all files in the summary-mix-test bucket using collection suffix agent01'. | Agent processes the request and invokes the index_data tool. |
| 3 | Wait for the index_data tool chipset to appear and complete. | Tool chipset visible with a completed state — not 'Tool execution failed'. |
| 4 | Click to expand the index_data tool chipset output. | Chipset detail view opens. |
| 5 | Verify the output includes ✅ Successfully indexed 3 documents (M chunks). | Line present; count = 3. |
| 6 | Verify the output includes a ⚠️ section listing the empty PDF and a ❌ section listing the corrupted file. | Both sections present with correct file names. |

## Expected Final State

Both sections present with correct file names.

## Pass/Fail Criteria

**Pass:**
- Chipset shows a completed state (not "Tool execution failed")
- Summary with ✅/⚠️/❌ sections visible in chipset output

**Fail:**
- Chipset shows "Tool execution failed"
- Chipset output contains only a raw count or generic string without per-section breakdown
