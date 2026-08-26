---
id: ELITEA-2816
title: "Tools Section Collapsed by Default with Enabled/Total Count"
priority: critical
type: functional
module: toolkits-indexes
status: ready
execution_type: manual
tags: [feat:toolkit-sections-redesign, tools, count, layout]
requirements: [EL-6252]
---
# ELITEA-2816: Tools Section Collapsed by Default with Enabled/Total Count

**Module:** Toolkits & Indexes · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that the Tools section is collapsed by default and displays the enabled/total tool count in the header.

**Coverage:**
- Tools section collapsed on page load
- Header shows "Tools" with count format "N / M"
- N = number of enabled tools
- M = total available tools for the toolkit
- Section can be expanded by clicking header

## Preconditions

- Logged in to {{base_url}}
- A toolkit with multiple tools exists (some enabled, some disabled)

## Test Data

| Field | Value |
|-------|-------|
| Toolkit | Any toolkit with multiple tools (e.g., GitHub, ADO with 20+ tools) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Toolkits & Indexes from the left sidebar. | Toolkits list page displays. |
| 2 | Click on a toolkit with multiple tools (e.g., GitHub). | Toolkit details page opens. |
| 3 | Observe the Tools section state on page load. | Tools section is collapsed by default. |
| 4 | Verify the Tools section header displays a count. | Header shows "Tools" with count (e.g., "Tools 16 / 33"). |
| 5 | Verify count format is "enabled / total". | Format shows enabled tools first, then total (e.g., "16 / 33"). |
| 6 | Click the Tools section header to expand. | Tools section expands showing all available tools. |
| 7 | Count the enabled tools (with toggles ON). | Count matches the first number in header. |
| 8 | Count total tools listed. | Count matches the second number in header. |

## Expected Final State

Tools section is collapsed by default with accurate enabled/total count displayed in header format "N / M".

## Pass/Fail Criteria

**Pass:**
- Tools section collapsed on page load
- Header shows count in "enabled / total" format
- Enabled count matches actual enabled tools
- Total count matches actual total tools
- Section expandable by clicking header

**Fail:**
- Tools section expanded on page load
- No count displayed in header
- Count format incorrect
- Count numbers don't match actual tools
