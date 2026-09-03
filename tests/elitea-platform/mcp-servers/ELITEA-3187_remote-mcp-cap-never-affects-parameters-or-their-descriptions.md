---
id: ELITEA-3187
title: "Remote MCP: max tool description length never affects tool parameters, their types, or their own descriptions"
priority: high
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp, feat:mcp-remote, r-2.0.6, issue:6016]
requirements: [EliteaAI/elitea_issues#6016]
---
# ELITEA-3187: Cap Is Scoped Only to the Top-Level Description

**Module:** Mcp Servers · **Priority:** High · **Type:** Functional

**Objective:** Verify that `Maximum tool description length` only shortens the tool's own top-level free-text description. A tool's parameters/arguments — their names, types, required flags, and each parameter's own description (e.g. a long enum-style parameter with a numbered list of options) — must remain completely intact and unaffected, and the agent must still be able to call the tool correctly.

## Preconditions

- User is logged into Elitea platform
- A Remote MCP toolkit is configured and connected to an external MCP server exposing a tool that has at least one parameter with a long description (e.g. an enum/string parameter documenting multiple option values)
- User has permission to edit the toolkit's configuration

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Open the Remote MCP toolkit's configuration and set `Maximum tool description length` to a small value (e.g. `50`) | Value is accepted and saved |
| 2 | Trigger tool discovery | Tools reload without error |
| 3 | Inspect the tool's parameter list (names, types, required/optional flags) | Unchanged from the tool's original schema — nothing renamed, retyped, or dropped |
| 4 | Inspect the long parameter's own description text | Full text preserved, with no shortening applied, regardless of the small cap set on the tool-level description |
| 5 | In chat, ask the agent to call the tool using that parameter with a valid value | Agent calls the tool correctly, passing the parameter as expected — the shortened top-level description did not prevent correct tool usage |

## Expected Final State

Only the tool's top-level description is shortened by the cap; parameter structure and parameter-level descriptions are untouched at any cap value, including very small ones.

## Pass/Fail Criteria

**Pass:** Parameters (structure and their own descriptions) are unaffected by any cap value; tool remains callable.
**Fail:** A parameter's name, type, required flag, or its own description is altered, dropped, or shortened because of the tool-level cap.
