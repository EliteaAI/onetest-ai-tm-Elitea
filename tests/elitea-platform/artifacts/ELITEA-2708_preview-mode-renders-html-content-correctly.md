---
id: ELITEA-2708
title: "Preview mode renders HTML content correctly"
priority: critical
type: functional
module: artifacts
status: draft
execution_type: manual
tags: [feat:artifacts, eng:frontend, r-2.0.4]
requirements: [EliteaAI/elitea_issues#5845]
---

## Preconditions

- User is logged in to `{{base_url}}`
- HTML file with rich content is available in Artifacts

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/` |
| Test file | test_file_2_between_1_3mb_structured.htm |
| Expected content | Comprehensive Test Report with Executive Dashboard |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open `test_file_2_between_1_3mb_structured.htm` in Preview mode | File opens in Canvas with rendered HTML |
| 2 | Verify headings render correctly (h1, h2, h3) | Headings display with proper hierarchy and styling |
| 3 | Verify text formatting (bold, italic, underlined, strikethrough, highlighted) | All text formatting styles are applied correctly |
| 4 | Verify dashboard cards with statistics are visible | 4 colored cards display (Total Revenue, Total Users, Performance, Engagement) |
| 5 | Scroll through and verify tables render correctly | Tables have proper borders, rows, and columns |
| 6 | Verify lists render correctly | Ordered and unordered lists display properly |
| 7 | Verify CSS styles are applied | Colors, fonts, spacing, and gradients match definitions |

## Expected Final State

- All HTML elements render correctly
- CSS styles are applied throughout the document
- No broken layouts or missing content
- Document is scrollable and readable

## Pass/Fail Criteria

**Pass:**
- All HTML elements (headings, text, tables, lists) render correctly
- CSS styles are applied (colors, fonts, spacing)
- Dashboard shows colored cards with statistics
- Text formatting showcase displays all styles correctly
- Tables have proper borders and structure

**Fail:**
- HTML elements render incorrectly or are missing
- CSS styles are not applied
- Layout is broken or content is missing
- Tables or lists do not render properly
