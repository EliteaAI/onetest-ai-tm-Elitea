---
id: ELITEA-1694
title: "Case-Insensitive Blocked Toolkit Matching"
priority: high
type: functional
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:admin-platform, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1694: Case-Insensitive Blocked Toolkit Matching

**Module:** Admin Portal / Guardrails · **Priority:** High · **Type:** Functional

**Objective:** Verify that blocked toolkit rules are applied correctly regardless of the casing used in tool invocations. The Guardrails enforcement should use case-insensitive, normalized matching.

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- An agent configured with a toolkit that supports multiple tools (e.g., `data_analysis`)
- MCP or external tool integration available that may use different casing conventions

## Test Data

| Configured Blocked Toolkit | Tool Invocation Variants to Test |
|---------------------------|----------------------------------|
| `data_analysis` | `Data_Analysis`, `DATA_ANALYSIS`, `data_Analysis`, `Data_analysis` |
| `GitHub` | `github`, `GITHUB`, `gitHub`, `Github` |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | In "Blocked Toolkits" section, add `data_analysis` toolkit. | Toolkit is added to the blocked list. |
| 3 | Click "Save Configuration". | Configuration saved successfully. |
| 4 | Open an agent chat that would normally use `data_analysis` toolkit. | Agent chat opens. |
| 5 | Send a prompt that triggers a tool from `data_analysis` toolkit. | Tool invocation is blocked. Agent cannot use tools from this toolkit. |
| 6 | (If MCP integration available) Configure an MCP server that exposes tools under `Data_Analysis` (different casing). | MCP server connected. |
| 7 | Send a prompt that triggers the MCP tool with `Data_Analysis` naming. | Tool is still blocked despite different casing. |
| 8 | Repeat test with `DATA_ANALYSIS` and `data_Analysis` variants. | All casing variants are blocked. |

## Expected Final State

All toolkit name variations (regardless of casing) that match the configured blocked toolkit are blocked by Guardrails.

## Pass/Fail Criteria

**Pass:**
- Blocked toolkit rule applies regardless of letter casing
- `data_analysis`, `Data_Analysis`, `DATA_ANALYSIS` all blocked when `data_analysis` is configured
- No enforcement gaps due to casing differences
- MCP tools with non-standard casing are correctly blocked

**Fail:**
- Some casing variants bypass the blocked toolkit rule
- Case-sensitive matching allows tools to execute when they should be blocked
- Inconsistent behavior between internal and MCP tools
