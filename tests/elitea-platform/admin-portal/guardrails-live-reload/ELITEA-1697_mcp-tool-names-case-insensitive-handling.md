---
id: ELITEA-1697
title: "MCP Tool Names with Non-Standard Casing Handled Correctly"
priority: high
type: functional
module: admin-portal/guardrails
status: ready
execution_type: manual
tags: [user_story:5199, feat:guardrails, feat:admin-platform, feat:mcp, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5199]
---
# ELITEA-1697: MCP Tool Names with Non-Standard Casing Handled Correctly

**Module:** Admin Portal / Guardrails · **Priority:** High · **Type:** Functional

**Objective:** Verify that Guardrails evaluates MCP toolkit and tool names using normalized, case-insensitive matching when the MCP server returns names in a casing or format not controlled by the platform.

## Preconditions

- Logged in as Platform Administrator
- Admin UI accessible
- MCP server configured that exposes tools with non-standard casing (e.g., PascalCase, UPPER_CASE, camelCase)
- Guardrails configured with blocked or sensitive tool rules

## Test Data

| MCP Server Tool Name | Platform Guardrails Config | Expected Behavior |
|---------------------|---------------------------|-------------------|
| `FileSystem_ReadFile` | Blocked: `filesystem_readfile` | Tool blocked |
| `DATABASE_QUERY` | Sensitive: `database_query` | Authorization required |
| `sendEmailNotification` | Blocked: `send_email_notification` | Tool blocked |
| `Create_New_Document` | Sensitive: `create_new_document` | Authorization required |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Admin UI → Configuration → Guardrails. | Guardrails configuration page loads. |
| 2 | Add `filesystem` to Blocked Toolkits with `readfile` blocked. | Configuration saved. |
| 3 | Add `database` toolkit with `query` tool to Sensitive Action Tools. | Configuration saved. |
| 4 | Connect an MCP server that exposes tools with different naming conventions (PascalCase, UPPER_CASE, etc.). | MCP server connected successfully. |
| 5 | Open agent chat with MCP toolkit enabled. | Agent chat opens, MCP tools available. |
| 6 | Send prompt that triggers `FileSystem_ReadFile` from MCP. | Tool is blocked. Guardrails recognizes it matches `filesystem_readfile`. |
| 7 | Send prompt that triggers `DATABASE_QUERY` from MCP. | Authorization dialog appears. Guardrails recognizes it matches `database_query`. |
| 8 | Test with camelCase variant `sendEmailNotification`. | Tool blocked if `send_email_notification` is in blocked list. |
| 9 | Verify the normalization handles underscores, hyphens, and casing together. | Rules apply correctly regardless of separator style. |

## Expected Final State

MCP tools with non-standard casing are correctly evaluated against Guardrails rules using normalized, case-insensitive matching.

## Pass/Fail Criteria

**Pass:**
- MCP tools are matched against Guardrails rules regardless of casing
- PascalCase, UPPER_CASE, camelCase, snake_case all normalized correctly
- Blocked rules block MCP tools with different casing
- Sensitive rules trigger authorization for MCP tools with different casing
- No false negatives where MCP tools bypass Guardrails due to naming differences

**Fail:**
- MCP tools bypass Guardrails due to casing differences
- Platform tools handled correctly but MCP tools with same logical name slip through
- Inconsistent normalization between different naming styles
