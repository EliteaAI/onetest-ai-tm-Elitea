---
id: ELITEA-4542
title: "Verify Tavily toolkit and credential display correctly across list, grid, table, and filtered views"
priority: medium
type: functional
module: tavily-toolkit
status: draft
execution_type: manual
tags: [feat:admin-platform, feat:chat, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6981]
---

## Preconditions

- A saved Tavily credential and toolkit

## Test Data

| View | Location |
|------|----------|
| List/grid | Credentials page |
| List/grid | Toolkits & Indexes page |
| Table view | Both pages, if available |
| Types filter | Both pages |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | View the Tavily credential in the Credentials list/grid | Shows name, "Tavily" type label, and a correctly rendered icon (no broken image) |
| 2 | View the Tavily toolkit in the Toolkits & Indexes list/grid | Shows name and correctly rendered icon |
| 3 | Switch to table view on both pages (if available) | Entries render correctly in table view too |
| 4 | Use the Types filter on both pages, filtering to "Tavily" | Only Tavily items are shown |

## Expected Final State

Tavily entries display consistently and correctly across all list/grid/table/filtered views.

## Pass/Fail Criteria

**Pass:**
- Name, type label, and icon render correctly in every view and filter mode

**Fail:**
- Any view shows a broken icon, missing label, or incorrect filter result
