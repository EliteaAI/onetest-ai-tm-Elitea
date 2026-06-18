---
id: ELITEA-0552
title: "Agent with Multiple Toolkits Added to Chat — Chipsets Show Full Traceback Content After Run Completion When Tools Receive Invalid Input Types"
priority: critical
type: functional
module: chipset-display
status: ready
execution_type: manual
tags: [nfr:validation, feat:pipelines, feat:toolkits, r-2.0.1]
requirements: [ProjectAlita/projectalita.github.io#3533]
---
# ELITEA-0552: Agent with Multiple Toolkits Added to Chat — Chipsets Show Full Traceback Content After Run Completion When Tools Receive Invalid Input Types

**Module:** Chipset Display · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that when an Agent with multiple toolkits is added as a participant to a Chat conversation and executed from Chat, each errored tool's chipset displays the full traceback — not empty output — both during and after the run completes.

**Coverage:**
- Agent with Confluence toolkit (`update_labels`) and GitHub toolkit (`index_data`) attached as a Chat participant
- `update_labels` called with `labels` as a plain string instead of array → ValidationError surfaced in chipset
- `index_data` called with `blacklist` as a string instead of array → ValidationError surfaced in chipset
- Each chipset opened **during** the run (while In Progress) shows the full traceback
- Each chipset opened **after** run completion still shows the full traceback — not empty
- Agent's final response in Chat includes the full exact error traceback for each failed tool call (unmodified)
- No chipset is blank or replaced with empty content after run ends

## Preconditions

- Logged in to {{base_url}} as Owner/Editor
- An Agent exists with the following toolkits attached:
  - **TaskConfluence** (Confluence toolkit) with `update_labels` tool enabled
  - **GithubMarian** (GitHub toolkit) with `index_data` tool enabled
- Agent instructions instruct it to: call `update_labels`, then call `index_data`, then produce a summary that includes the full exact error traceback for every tool run without changes
- A Chat conversation exists (or is created) with the agent added as a participant

## Test Data

| Tool | Toolkit | Parameter | Invalid Value | Expected Error Cause |
|---|---|---|---|---|
| `update_labels` | TaskConfluence | `page_ids` | `["39813121","40665089"]` (list — valid) | — |
| `update_labels` | TaskConfluence | `labels` | `"abc"` (string) | Expected array, got string → ValidationError |
| `index_data` | GithubMarian | `index_name` | `"name"` (string — valid) | — |
| `index_data` | GithubMarian | `blacklist` | `"123"` (string) | Expected array, got string → ValidationError |

Agent instruction prompt:
1. Call update_labels on TaskConfluence with pages ["39813121","40665089"] and labels "abc"
2. Call index_data on GithubMarian with index_name "name" and blacklist "123"
3. Give a summary of what was done. In the summary include the full exact error traceback if it exists — provide it fully without any changes for every tool run.

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Chat and open an existing conversation or create a new one. | Chat conversation view is open. |
| 2 | Add the configured Agent (with TaskConfluence and GithubMarian toolkits) as a participant to the conversation using the Participants panel. | Agent appears as a participant in the conversation. Both toolkits are reflected in the participants panel. |
| 3 | Send the prompt instructing the agent to: (1) call update_labels on TaskConfluence with pages ["39813121","40665089"] and labels "abc", (2) call index_data on GithubMarian with index_name "name" and blacklist "123", (3) provide a full summary including exact error tracebacks. | Agent begins execution from Chat; run is In Progress; toolkit calls are initiated. |
| 4 | While the run is In Progress, click the chipset for the `update_labels` tool execution in the Chat message thread. | Chipset opens and displays the Pydantic ValidationError traceback (field `labels`, error details) — not empty. |
| 5 | While the run is still In Progress, click the chipset for the `index_data` tool execution in the Chat message thread. | Chipset opens and displays the Pydantic ValidationError traceback (field `blacklist`, error details) — not empty. |
| 6 | Wait for the Agent run to fully complete. | Run reaches terminal state; agent produces a summary response in the Chat conversation. |
| 7 | After completion, re-open the chipset for the `update_labels` execution. | Chipset still shows the full traceback content from step 4 — identical content, not empty. |
| 8 | After completion, re-open the chipset for the `index_data` execution. | Chipset still shows the full traceback content from step 5 — identical content, not empty. |
| 9 | Read the agent's final summary response in the Chat. | Response includes the full, exact, unmodified error traceback text for both tool calls (`update_labels` and `index_data`) as instructed. |

## Expected Final State

Response includes the full, exact, unmodified error traceback text for both tool calls (`update_labels` and `index_data`) as instructed.

## Pass/Fail Criteria

**Pass:**
- Both chipsets are non-empty during run and remain non-empty after completion when agent is invoked from Chat
- Chipset content post-run is identical to mid-run content (no data lost on completion)
- Agent response in Chat includes the full verbatim traceback for both failed tool calls

**Fail:**
- Either chipset is empty after run completion while it was non-empty during run
- Chipset content is truncated or replaced with generic "No output" after run ends
- Agent response omits traceback or shows truncated error info
