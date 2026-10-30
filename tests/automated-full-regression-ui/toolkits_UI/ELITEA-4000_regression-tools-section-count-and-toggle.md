---
id: ELITEA-4000
title: "Regression - Tools Section Count Updates and Header Toggle"
priority: critical
type: regression
module: toolkits-indexes
status: draft
execution_type: manual
tags: [regression, smoke, toolkit-sections-redesign, tools, feat:toolkits, r-2.0.8]
requirements: [EL-6252, EliteaAI/elitea_issues#7045]
---
# ELITEA-4000: Regression - Tools Section Count Updates and Header Toggle

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Regression / Smoke

**Objective:** Verify Tools section is expanded by default, its header is clickable for collapse/expand, and enabling/disabling tools updates the count in real-time.

**Coverage:**
- Tools section expanded by default (changed by EliteaAI/elitea_issues#7045)
- Tools section header clickable
- Collapse/expand works correctly
- Tool enable/disable updates header count immediately
- Count format "enabled / total" is accurate

## Preconditions

- Logged in to {{base_url}} with edit permissions
- A toolkit with multiple tools (some enabled, some disabled)
- Test is run in a fresh incognito window (no earlier collapse of the section in this browser)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with 10+ tools |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes → open a toolkit. | Toolkit details page opens. |
| 2 | Observe Tools section is expanded. | Section expanded showing all tools, with count visible. |
| 3 | Note the count (e.g., "16 / 33"). | Initial count recorded. |
| 4 | Verify count of enabled tools matches header. | Enabled count accurate. |
| 5 | Disable one enabled tool (toggle OFF). | Tool disabled. |
| 6 | Verify header count decrements immediately (e.g., "15 / 33"). | Count updates without refresh. |
| 7 | Enable the tool back (toggle ON). | Tool enabled. |
| 8 | Verify header count increments (e.g., "16 / 33"). | Count updates correctly. |
| 9 | Click Tools section header. | Section collapses; count stays visible. |
| 10 | Click Tools section header again. | Section expands showing all tools. |

## Expected Final State

Tools section is expanded by default, header toggles collapse/expand, and tool count updates in real-time.

## Pass/Fail Criteria

**Pass:**
- Section expanded on page load
- Header click toggles section
- Count updates immediately on toggle
- Count format is correct
- Total count unchanged

**Fail:**
- Section collapsed on page load
- Header not clickable
- Count doesn't update
- Wrong count numbers
- Requires page refresh
