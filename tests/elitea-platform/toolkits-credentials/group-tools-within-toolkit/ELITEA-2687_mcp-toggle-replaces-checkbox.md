---
id: ELITEA-2687
title: "MCP Access Toggle Replaces Checkbox with Correct Default State"
priority: critical
type: functional
module: toolkits-credentials/group-tools-within-toolkit
status: ready
execution_type: manual
tags: [feat:toolkits, tools, mcp, toggle]
requirements: []
refs:
  - https://github.com/EliteaAI/elitea_issues/issues/2677
  - https://github.com/EliteaAI/elitea_issues/issues/6253
---
# ELITEA-2687: MCP Access Toggle Replaces Checkbox with Correct Default State

**Module:** Toolkits Credentials / Group Tools Within Toolkit · **Priority:** Critical · **Type:** Functional

**Objective:** Verify the MCP checkbox is replaced with a toggle at the end of the Tools section with correct label and default behavior.

**Coverage:**
- MCP control is a toggle, not a checkbox
- Toggle is at the end of the Tools section
- Label is "Enable MCP access for selected tools"
- New toolkits default to toggle OFF
- Existing toolkits preserve their previous MCP setting

## Preconditions

- Logged in to {{base_url}}
- User has access to ELITEA platform
- User is in Private project context
- At least one existing toolkit with MCP previously enabled exists

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Toolkits page and click **"Create Toolkit"** to create a new SDK toolkit. | Toolkit creation form opens. |
| 2 | Select a toolkit type (e.g., Jira) and configure basic settings and credentials. | Form fields populate based on selected type. |
| 3 | Scroll to the **Tools section** and locate the MCP control at the end. | A **toggle** (not checkbox) is located at the **END** of the Tools section, after all tool groups. |
| 4 | Verify the toggle label and default state. | Toggle label reads **"Enable MCP access for selected tools"**. Toggle is **OFF** (disabled) by default. |
| 5 | Verify info icon is present next to the toggle and hover over it. | ⓘ icon is present. Hovering shows an **explanatory tooltip** about MCP functionality. |
| 6 | Cancel toolkit creation and open an **existing toolkit** that had "Make tools available by MCP" previously enabled. | Existing toolkit configuration page opens. |
| 7 | Verify the MCP control type and state on existing toolkit. | Control is a **toggle** (not a checkbox). Toggle state is **ON** (preserving existing setting). |
| 8 | Verify the toggle label on existing toolkit. | Label is **"Enable MCP access for selected tools"** (same as new toolkit). |

## Expected Final State

MCP toggle displays correctly on both new and existing toolkits with appropriate default/preserved states.

## Pass/Fail Criteria

**Pass:**
- MCP control is a toggle, not a checkbox
- Toggle is positioned at the end of the Tools section
- Label reads "Enable MCP access for selected tools"
- New toolkits default to toggle OFF
- Existing toolkits with MCP enabled show toggle ON (setting preserved)
- Info icon with tooltip is present

**Fail:**
- MCP control is still a checkbox
- Toggle is not at the end of the Tools section
- Label text is incorrect
- New toolkit defaults to toggle ON
- Existing toolkit's MCP setting is not preserved
