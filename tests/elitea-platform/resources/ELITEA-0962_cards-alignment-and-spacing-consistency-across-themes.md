---
id: ELITEA-0962
title: "Cards Alignment and Spacing Consistency Across Themes"
priority: medium
type: functional
module: resources
status: ready
execution_type: manual
tags: [user_story:4771, feat:settings, 4771]
requirements: [EliteaAI/elitea_issues#4771]
---
# ELITEA-0962: Cards Alignment and Spacing Consistency Across Themes

**Module:** Resources · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that card alignment, inter-card spacing, and inner padding are visually consistent across all 4 cards in both Light Mode and Dark Mode at a standard viewport width.

**Coverage:**
- Equal height or visually balanced cards
- Consistent horizontal and vertical gaps between cards
- Uniform inner padding (icon-to-title, title-to-links) across all cards
- No layout shift between Light and Dark themes

## Preconditions

Logged in to ELITEA; on the Resources page
Browser window set to 1280px wide

## Test Data

Viewport: 1280px wide
Check both Light Mode and Dark Mode

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Resources page at 1280px width in Light Mode. | Resources page loads with 4 cards in 2×2 grid. |
| 2 | Visually inspect card heights: confirm all 4 cards appear equal in height or visually balanced. | Cards appear uniform in height. |
| 3 | Inspect horizontal spacing between the two columns: confirm equal gap on both sides. | Column gap is equal left and right. |
| 4 | Inspect vertical spacing between the top and bottom rows: confirm it is consistent with horizontal spacing. | Row gap matches column gap visually. |
| 5 | Switch to Dark Mode and repeat alignment checks. | Card alignment, spacing, and padding are identical in Dark Mode. No layout shift occurred on theme switch. |

## Expected Final State

Card alignment, spacing, and padding are identical in Dark Mode. No layout shift occurred on theme switch.

## Pass/Fail Criteria

**Pass:**
- All 4 cards appear visually balanced in height at 1280px
- Horizontal spacing between columns is equal on both sides
- Vertical spacing between rows matches horizontal spacing
- Inner card padding is uniform across all cards
- No layout shift between Light and Dark modes

**Fail:**
- Cards have mismatched heights causing visual imbalance
- Column/row spacing is uneven
- Inner padding differs noticeably between cards
- A layout shift or misalignment appears when switching themes
