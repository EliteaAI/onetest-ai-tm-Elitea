---
id: ELITEA-1696
title: "Case-Insensitive Sensitive Action Tool Matching"
priority: high
type: functional
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1696: Case-Insensitive Sensitive Action Tool Matching

**Module:** Admin Portal / Guardrails · **Priority:** High · **Type:** Functional

**Objective:** Verify that Sensitive Action Tool rules trigger the authorization dialog correctly regardless of the casing used in tool invocations.

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- An agent with access to a toolkit containing tools to be marked as sensitive (e.g., `data_analysis` toolkit with `pandas_analyze_data` tool)

## Test Data

| Toolkit | Configured Sensitive Tool | Tool Invocation Variants to Test |
|---------|--------------------------|----------------------------------|
| `data_analysis` | `pandas_analyze_data` | `Pandas_Analyze_Data`, `PANDAS_ANALYZE_DATA`, `pandasAnalyzeData` |
| `github` | `delete_branch` | `Delete_Branch`, `DELETE_BRANCH`, `deleteBranch` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | In "Sensitive Action Tools" section, select `data_analysis` toolkit and mark `pandas_analyze_data` as sensitive. | Tool is added to sensitive tools list. |
| 3 | Click "Save Configuration". | Configuration saved successfully. |
| 4 | Open an agent chat with `data_analysis` toolkit enabled. | Agent chat opens. |
| 5 | Send a prompt that triggers `pandas_analyze_data` tool. | Authorization dialog appears before tool execution. |
| 6 | Click "Authorize" in the dialog. | Tool executes successfully. |
| 7 | (If MCP integration) Configure MCP server that exposes `Pandas_Analyze_Data` (different casing). | MCP server connected. |
| 8 | Send a prompt that triggers the MCP tool with different casing. | Authorization dialog still appears. Sensitive rule applied correctly. |
| 9 | Test with `PANDAS_ANALYZE_DATA` variant. | Authorization dialog appears. |

## Expected Final State

The authorization dialog is triggered for all casing variations of the configured sensitive tool name.

## Pass/Fail Criteria

**Pass:**
- Authorization dialog appears for all casing variants of the sensitive tool
- `pandas_analyze_data`, `Pandas_Analyze_Data`, `PANDAS_ANALYZE_DATA` all trigger authorization
- Dialog content is correct regardless of tool name casing
- Tool executes after authorization is granted

**Fail:**
- Some casing variants bypass the authorization requirement
- Authorization dialog does not appear for MCP tools with different casing
- Inconsistent authorization behavior based on tool name format
