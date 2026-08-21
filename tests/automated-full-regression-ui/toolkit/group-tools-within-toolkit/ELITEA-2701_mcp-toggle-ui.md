---
id: ELITEA-2701
title: "MCP Toggle UI and Default State"
priority: critical
type: functional
module: toolkit/group-tools-within-toolkit
status: draft
execution_type: manual
tags: [feat:toolkits, tools, mcp, toggle]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2701: MCP Toggle UI and Default State

**Module:** Toolkit / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify MCP access control is a toggle (not checkbox) at the end of Tools section with correct label and default OFF state for new toolkits.

**Coverage:**
- MCP control is a toggle, not checkbox
- Toggle positioned at end of Tools section
- Label "Enable MCP access for selected tools"
- Info icon with tooltip present
- Default OFF for new toolkit

## Preconditions

- Logged in to {{base_url}}
- User has access to create toolkits
- User is in Private project context

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits page and click **"Create Toolkit"**. | Toolkit creation form opens. |
| 2 | Select a toolkit type (e.g., Jira) and configure required fields. | Form populates with fields. |
| 3 | Scroll to Tools section and locate MCP control at the **end** (after all tool groups). | MCP control is a **toggle** (not checkbox), positioned at **end** of Tools section. |
| 4 | Verify toggle label. | Label: **"Enable MCP access for selected tools"**. |
| 5 | Verify toggle default state. | Toggle is **OFF** by default. |
| 6 | Verify info icon next to toggle and hover over it. | ⓘ icon present. Tooltip shows explanatory text about MCP. |
| 7 | Toggle it ON, save the toolkit. | Save completes successfully. |
| 8 | Reopen the toolkit. | Toggle is **ON** (state persisted). |
| 9 | Toggle it OFF, save and reopen. | Toggle is **OFF** (state persisted). |

## Expected Final State

MCP toggle displays correctly with proper label, default state, and persistence.

## Pass/Fail Criteria

**Pass:**
- MCP control is a toggle (not checkbox)
- Toggle at end of Tools section
- Label "Enable MCP access for selected tools"
- Info icon with tooltip present
- Default OFF for new toolkit
- State persists after save

**Fail:**
- MCP control is checkbox
- Toggle not at end of section
- Wrong label
- Missing info icon
- Default ON for new toolkit
- State not persisted
