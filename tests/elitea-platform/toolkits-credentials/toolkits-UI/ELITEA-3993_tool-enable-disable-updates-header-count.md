---
id: ELITEA-3993
title: "Tool Enable/Disable Updates Header Count in Real-Time"
priority: high
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, tools, count, toggle]
requirements: [EL-6252]
---
# ELITEA-3993: Tool Enable/Disable Updates Header Count in Real-Time

**Module:** Toolkits & Indexes · **Priority:** High · **Type:** Functional

**Objective:** Verify that enabling or disabling a tool immediately updates the count in the Tools section header.

**Coverage:**
- Disabling a tool decrements enabled count
- Enabling a tool increments enabled count
- Total count remains unchanged
- Count updates in real-time without page refresh

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with multiple tools (some enabled, some disabled)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with multiple tools |
| Initial Count | Note the starting enabled/total count |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → open a toolkit with multiple tools. | Toolkit details page opens. |
| 2 | Observe the Tools section header count (e.g., "16 / 33"). | Initial count noted. |
| 3 | Expand the Tools section by clicking the header. | Tools list appears with toggle switches. |
| 4 | Locate an enabled tool (toggle ON). | Enabled tool found. |
| 5 | Toggle the tool OFF (disable it). | Tool is disabled. |
| 6 | Immediately observe the header count. | Enabled count decrements by 1 (e.g., "15 / 33"). |
| 7 | Locate a disabled tool (toggle OFF). | Disabled tool found. |
| 8 | Toggle the tool ON (enable it). | Tool is enabled. |
| 9 | Immediately observe the header count. | Enabled count increments by 1 (e.g., "16 / 33"). |
| 10 | Verify total count remains unchanged. | Total count stays the same (e.g., still "33"). |

## Expected Final State

Header count accurately reflects enabled tools in real-time as tools are toggled on/off.

## Pass/Fail Criteria

**Pass:**
- Disabling tool decrements enabled count immediately
- Enabling tool increments enabled count immediately
- Total count unchanged
- No page refresh required for count update

**Fail:**
- Count doesn't update on toggle
- Count updates only after page refresh
- Total count changes incorrectly
- Count shows wrong numbers
