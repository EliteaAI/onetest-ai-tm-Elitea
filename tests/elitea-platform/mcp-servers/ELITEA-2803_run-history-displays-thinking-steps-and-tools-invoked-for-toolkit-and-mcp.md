---
id: ELITEA-2803
title: "Run History displays Thinking Steps and Tools Invoked for Toolkit and MCP"
priority: high
type: functional
module: mcp-servers
status: ready
execution_type: manual
tags: [feat:mcp, feat:toolkits, bug:6345, r-2.0.2]
requirements: [EliteaAI/elitea_issues#6345]
---
# ELITEA-2803: Run History displays Thinking Steps and Tools Invoked for Toolkit and MCP

**Module:** MCP Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that Run History for Toolkits and MCPs displays thinking steps (including duration), tools invoked with toolkit/MCP name, and execution results consistent with Agent Run History.

**Coverage:**
- Toolkit Run History shows "Thought for X secs" section
- Toolkit Run History shows tools invoked with toolkit name and action
- MCP Run History shows "Thought for X secs" section
- MCP Run History shows tools invoked with MCP name and action
- Thinking content is expandable and displays LLM reasoning
- Execution trace is preserved and not lost after run completion

## Preconditions

- Logged in to {{base_url}} with owner or editor access on a Private project
- A Toolkit with at least one completed tool execution exists
- An MCP server with at least one completed tool execution exists

## Test Data

| Field | Value |
|-------|-------|
| Toolkit type | Any toolkit with completed runs (e.g., ADO Wiki, GitHub, Jira) |
| MCP server | Any MCP with completed runs |

## Steps

### Part A: Toolkit Run History

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits & Indexes in the left navigation menu. | Toolkits list is displayed. |
| 2 | Open a Toolkit that has completed tool executions (not indexing). | Toolkit detail page opens. |
| 3 | Click on "Run History" in the page header or history icon. | Run History panel opens showing a list of past operations. |
| 4 | Click on a completed run entry in the list. | Right panel expands to show execution details. |
| 5 | Verify the thinking steps section is displayed. | "Thought for X secs" label is visible with an expand/collapse arrow. |
| 6 | Click on the thinking steps section to expand it. | Modal/panel opens showing full thinking text with reasoning content. |
| 7 | Verify thinking content is readable and formatted. | Text is complete, no truncation, displays LLM reasoning process. |
| 8 | Verify the tools invoked section shows the toolkit name and action. | Tools invoked displays as "[Toolkit Name]: [tool_action]" (e.g., "GitHub: get_issue"). |

### Part B: MCP Run History

| # | Action | Expected Result |
|---|--------|----------------|
| 9 | Navigate to MCPs in the left navigation menu. | MCPs list is displayed. |
| 10 | Open an MCP server that has completed tool executions. | MCP detail page opens. |
| 11 | Click on "Run History" in the page header or history icon. | Run History panel opens showing a list of past operations. |
| 12 | Click on a completed run entry in the list. | Right panel expands to show execution details. |
| 13 | Verify the thinking steps section is displayed. | "Thought for X secs" label is visible with an expand/collapse arrow. |
| 14 | Click on the thinking steps section to expand it. | Modal/panel opens showing full thinking text with reasoning content. |
| 15 | Verify thinking content is readable and formatted. | Text is complete, no truncation, displays LLM reasoning process. |
| 16 | Verify the tools invoked section shows the MCP name and action. | Tools invoked displays as "[MCP Name]: [tool_action]". |

### Part C: Consistency Check

| # | Action | Expected Result |
|---|--------|----------------|
| 17 | Navigate to Agents and open an Agent with completed runs. | Agent detail page opens. |
| 18 | Open Run History for the Agent. | Agent Run History panel opens. |
| 19 | Compare the thinking steps display format between Agent, Toolkit, and MCP Run History. | Thinking steps format is consistent across all three entity types. |
| 20 | Compare the tools invoked display format between Agent, Toolkit, and MCP Run History. | Tools invoked format is consistent across all three entity types. |

## Expected Final State

Run History for Toolkits and MCPs displays:
- "Thought for X secs" section with expandable thinking content
- Tools invoked showing "[Entity Name]: [tool_action]" format
- Complete execution trace without missing intermediate steps
- Consistent format with Agent Run History

## Pass/Fail Criteria

**Pass:**
- Toolkit Run History displays thinking steps with "Thought for X secs" label
- Toolkit Run History displays tools invoked with toolkit name and action
- MCP Run History displays thinking steps with "Thought for X secs" label
- MCP Run History displays tools invoked with MCP name and action
- Thinking content is expandable and shows LLM reasoning
- Format is consistent with Agent Run History

**Fail:**
- Thinking steps are missing from Toolkit or MCP Run History
- Tools invoked section is missing or shows incorrect format
- Thinking content cannot be expanded or is truncated
- Run History only shows request parameters and final results without execution trace
- Format differs significantly from Agent Run History
