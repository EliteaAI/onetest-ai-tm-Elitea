---
id: ELITEA-3186
title: "Remote MCP: negative max tool description length value is rejected by the config form"
priority: medium
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp, feat:mcp-remote, r-2.0.6, issue:6016]
requirements: [EliteaAI/elitea_issues#6016]
---
# ELITEA-3186: Negative Cap Value Is Rejected

**Module:** Mcp Servers · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that entering a negative number into `Maximum tool description length` on a Remote MCP toolkit is rejected by the configuration form (the field's schema requires `>= 0`), rather than being silently saved or crashing tool creation.

## Preconditions

- User is logged into Elitea platform
- A Remote MCP toolkit is configured
- User has permission to edit the toolkit's configuration

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the Remote MCP toolkit's configuration | Configuration form loads |
| 2 | Enter a negative value (e.g. `-1`) into `Maximum tool description length` | Form either blocks the character/value entry or shows a validation error |
| 3 | Attempt to save the toolkit with the negative value present | Save is blocked with a clear validation message, or the value is coerced back to a valid default (`0`) — not silently accepted as-is |
| 4 | If save was somehow allowed, trigger tool discovery | Toolkit still discovers tools correctly (treated as unlimited/`0`), no crash |

## Expected Final State

A negative cap can never reach the SDK as a saved, honored value that breaks tool discovery.

## Pass/Fail Criteria

**Pass:** Negative value is rejected at the form, or if it somehow persists, discovery still works correctly (treated as unlimited).
**Fail:** Negative value is saved and causes an error, crash, or broken tool discovery.
