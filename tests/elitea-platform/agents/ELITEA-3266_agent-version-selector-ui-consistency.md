---
id: ELITEA-3266
title: "Agent — Version Selector UI Consistency"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:version-selector, nfr:ui-consistency, feat:agents, issue:6302]
requirements: [EliteaAI/elitea_issues#6302]
---
# ELITEA-3266: Agent — Version Selector UI Consistency

**Module:** Agents · **Priority:** High · **Type:** Functional

**Objective:** Verify that the version selector dropdown has consistent styling, layout, and behavior, serving as the baseline reference for comparison with Pipelines and Skills.

## Preconditions

- User logged in to ELITEA ({{base_url}})
- Agent exists with multiple versions

## Test Data

| Field | Value |
|-------|-------|
| Test Agent | Agent with ≥3 versions |
| UI Elements to Verify | Dropdown width, row height, font sizes, icon sizes, spacing, search input field |

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to the Agent configuration page | Agent page loads |
| 2 | Open the version selector dropdown | Dropdown opens |
| 3 | Measure and note dropdown width | Dropdown width is appropriate (not too narrow or wide) |
| 4 | Measure and note row height for version entries | Row height is consistent across all version entries |
| 5 | Verify font sizes are readable and consistent | Version names, timestamps, creator info use consistent, readable fonts |
| 6 | Verify icon sizes (checkmark, pin) are consistent | All icons are same size and properly aligned |
| 7 | Verify spacing between elements | Consistent padding/margin between rows and within rows |
| 8 | Verify search input field styling | Search field has clear border, appropriate height, visible placeholder |
| 9 | Verify metadata display layout | Name, timestamp, creator info are properly aligned and spaced |
| 10 | Verify icon positioning (checkmark, pin) | Icons are aligned consistently within each row |

## Expected Final State

Version selector dropdown has consistent, professional styling; all elements are properly sized, spaced, and aligned.

## Pass/Fail Criteria

**Pass:** Dropdown width, row height, fonts, icons, and spacing are consistent; layout is clean and professional

**Fail:** Inconsistent sizing or spacing; misaligned icons; poor readability; unprofessional appearance

**Note:** This test establishes the baseline for Agents. Results will be compared with Pipelines (ELITEA-TBD) and Skills (ELITEA-TBD) to verify cross-component consistency.
