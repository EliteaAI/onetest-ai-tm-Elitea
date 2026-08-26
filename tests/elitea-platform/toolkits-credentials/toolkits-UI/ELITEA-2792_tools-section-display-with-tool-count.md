---
id: ELITEA-2792
title: "TOOLS Section Display with Tool Count"
priority: medium
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-redesign, tools, count]
requirements: []
---
# ELITEA-2792: TOOLS Section Display with Tool Count

**Module:** Toolkits & Indexes · **Priority:** Medium · **Type:** Functional

**Objective:** Verify TOOLS section shows correct count format and tool list.

**Coverage:**
- TOOLS section visible in left panel
- Count format shows "N/M" (enabled/total)
- Tools can be enabled/disabled
- Count updates on toggle changes

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with multiple tools available

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with multiple tools (e.g., GitHub, ADO) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → select a toolkit. | Toolkit details page opens. |
| 2 | Locate the TOOLS section in the left panel. | TOOLS section visible with header showing count (e.g., "TOOLS 20/22"). |
| 3 | Verify the count format. | Format is "N/M" where N = enabled tools, M = total tools. |
| 4 | Expand the TOOLS section if collapsed. | Tool list becomes visible with toggles. |
| 5 | Observe individual tool entries. | Each tool has a name, toggle switch, and possibly description. |
| 6 | Disable one enabled tool by toggling it off. | Tool is disabled; count updates (e.g., "19/22"). |
| 7 | Enable the tool again. | Tool is enabled; count updates back (e.g., "20/22"). |
| 8 | Verify the count reflects actual enabled/total tools. | Count is accurate. |

## Expected Final State

TOOLS section displays correct count format that updates dynamically when tools are enabled/disabled.

## Pass/Fail Criteria

**Pass:**
- TOOLS section visible
- Count format is "enabled/total"
- Toggle changes update count immediately
- Count is accurate

**Fail:**
- TOOLS section missing
- Wrong count format
- Count doesn't update on toggle
- Count is inaccurate
