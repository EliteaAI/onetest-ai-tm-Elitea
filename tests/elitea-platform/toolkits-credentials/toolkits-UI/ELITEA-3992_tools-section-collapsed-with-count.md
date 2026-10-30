---
id: ELITEA-3992
title: "Tools Section Expanded by Default with Enabled/Total Count"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, feat:toolkits, tools, count, layout, r-2.0.8]
requirements: [EL-6252, EliteaAI/elitea_issues#7045]
---
# ELITEA-3992: Tools Section Expanded by Default with Enabled/Total Count

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Tools section is expanded by default and displays the enabled/total tool count in the header.

**Coverage:**
- Tools section expanded on page load (changed by EliteaAI/elitea_issues#7045; previously collapsed)
- Header shows "Tools" with count format "N / M"
- N = number of enabled tools
- M = total available tools for the toolkit
- Section can be collapsed and expanded again by clicking header

## Preconditions

- Logged in to {{base_url}}
- A toolkit with multiple tools exists (some enabled, some disabled)
- Test is run in a fresh incognito window (no earlier collapse of the section in this browser)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with multiple tools (e.g., GitHub, ADO with 20+ tools) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes from the left sidebar. | Toolkits list page displays. |
| 2 | Click on a toolkit with multiple tools (e.g., GitHub). | Toolkit details page opens. |
| 3 | Observe the Tools section state on page load. | Tools section is expanded by default and all tool cards are visible. |
| 4 | Verify the Tools section header displays a count. | Header shows "Tools" with count (e.g., "Tools 16 / 33"). |
| 5 | Verify count format is "enabled / total". | Format shows enabled tools first, then total (e.g., "16 / 33"). |
| 6 | Count the enabled tools (with toggles ON). | Count matches the first number in header. |
| 7 | Count total tools listed. | Count matches the second number in header. |
| 8 | Click the Tools section header. | Tools section collapses; the count stays visible in the header. |
| 9 | Click the Tools section header again. | Tools section expands showing all available tools. |

## Expected Final State

Tools section is expanded by default with accurate enabled/total count displayed in header format "N / M".

## Pass/Fail Criteria

**Pass:**
- Tools section expanded on page load
- Header shows count in "enabled / total" format
- Enabled count matches actual enabled tools
- Total count matches actual total tools
- Section collapses and expands by clicking header

**Fail:**
- Tools section collapsed on page load
- No count displayed in header
- Count format incorrect
- Count numbers don't match actual tools
