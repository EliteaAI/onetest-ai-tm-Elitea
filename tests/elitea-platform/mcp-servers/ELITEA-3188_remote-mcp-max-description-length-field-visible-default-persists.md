---
id: ELITEA-3188
title: "Remote MCP: max tool description length field is visible in toolkit settings, defaults empty, and saves correctly"
priority: medium
type: functional
module: mcp-servers
status: draft
execution_type: manual
tags: [feat:mcp, feat:mcp-remote, r-2.0.6, issue:6016]
requirements: [EliteaAI/elitea_issues#6016]
---
# ELITEA-3188: Config Field Visibility, Default, and Save

**Module:** Mcp Servers · **Priority:** Medium · **Type:** Functional

**Objective:** Verify the `Maximum tool description length` (or equivalent label) field is present in the Remote MCP toolkit's settings form, defaults to empty/`0`, has legible helper/tooltip text, and saving a numeric value does not produce a validation error on save (this field is typed as a plain integer, unlike sibling fields such as `timeout`/`cache_ttl` that accept int-or-string).

## Preconditions

- User is logged into Elitea platform
- User has permission to create/edit a Remote MCP toolkit

## Steps

| # | Action | Expected Result |
|---|--------|------------------|
| 1 | Navigate to Toolkits → MCPs and open a Remote MCP toolkit's configuration (or create a new one) | Configuration form loads |
| 2 | Locate the `Maximum tool description length` field | Field is present and, on a fresh/unconfigured toolkit, is empty (default unlimited) |
| 3 | Hover/inspect the field's tooltip or helper text | Text is legible and describes the field's purpose |
| 4 | Enter a numeric value (e.g. `300`) into the field and save the toolkit | Save succeeds with no validation error |
| 5 | Reload the page and reopen the toolkit's configuration | The saved value (`300`) is still displayed |

## Expected Final State

The field is discoverable, defaults sensibly, and a numeric value round-trips through save/reload correctly.

## Pass/Fail Criteria

**Pass:** Field is visible with legible help text, defaults to empty, and a numeric value saves and persists without error.
**Fail:** Field is missing/hidden, save produces a validation error for a valid numeric value, or the saved value does not persist after reload.
