---
id: ELITEA-2824
title: "Regression - Tools Section Count Updates and Header Toggle"
priority: critical
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, smoke, toolkit-sections-redesign, tools]
requirements: [EL-6252]
---
# ELITEA-2824: Regression - Tools Section Count Updates and Header Toggle

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Regression / Smoke

**Objective:** Verify Tools section header is clickable for expand/collapse, and enabling/disabling tools updates the count in real-time.

**Coverage:**
- Tools section header clickable
- Expand/collapse works correctly
- Tool enable/disable updates header count immediately
- Count format "enabled / total" is accurate

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with multiple tools (some enabled, some disabled)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with 10+ tools |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → open a toolkit. | Toolkit details page opens. |
| 2 | Observe Tools section is collapsed. | Section collapsed with count visible. |
| 3 | Note the count (e.g., "16 / 33"). | Initial count recorded. |
| 4 | Click Tools section header. | Section expands showing all tools. |
| 5 | Verify count of enabled tools matches header. | Enabled count accurate. |
| 6 | Disable one enabled tool (toggle OFF). | Tool disabled. |
| 7 | Verify header count decrements immediately (e.g., "15 / 33"). | Count updates without refresh. |
| 8 | Enable the tool back (toggle ON). | Tool enabled. |
| 9 | Verify header count increments (e.g., "16 / 33"). | Count updates correctly. |
| 10 | Click Tools section header again. | Section collapses. |

## Expected Final State

Tools section header toggles expand/collapse, and tool count updates in real-time.

## Pass/Fail Criteria

**Pass:**
- Header click toggles section
- Count updates immediately on toggle
- Count format is correct
- Total count unchanged

**Fail:**
- Header not clickable
- Count doesn't update
- Wrong count numbers
- Requires page refresh
