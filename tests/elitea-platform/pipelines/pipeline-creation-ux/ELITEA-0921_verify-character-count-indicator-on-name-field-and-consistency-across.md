---
id: ELITEA-0921
title: "Verify Character Count Indicator on Name Field and Consistency Across Fields"
priority: medium
type: functional
module: pipeline-creation-ux
status: ready
execution_type: manual
tags: [feat:pipelines, r-2.0.2, 4418, 4688]
requirements: [EliteaAI/elitea_issues#4418, EliteaAI/elitea_issues#4688]
---
# ELITEA-0921: Verify Character Count Indicator on Name Field and Consistency Across Fields

**Module:** Pipeline Creation Ux · **Priority:** Medium · **Type:** Functional

**Objective:** Verify that the Name field shows a character count indicator when approaching its limit (~32 characters), and that the Description and Welcome Message fields show character count indicators consistently.

**Coverage:**
- Character count indicator behavior on Name field
- Character count indicator consistency across Name, Description, and Welcome Message fields
- Name field character limit threshold (~32 chars)

## Preconditions

- Logged in
- Private project selected
- New Pipeline creation form (or Agent creation form) is open

## Test Data

Field | Short value (below threshold) | Near-limit value (≥32 chars)
Name | ShortName | This pipeline name is thirty-two
Description | Short desc | Any text close to its limit
Welcome Message | Hi | Any text close to its limit

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Open the Create New Pipeline form | Form is displayed |
| 2 | Click into the Name field and type a short string (ShortName, 9 chars) | No character count indicator appears (below threshold) |
| 3 | Continue typing in the Name field until reaching 32+ characters (This pipeline name is thirty-two) | Character count indicator appears, showing remaining or used characters |
| 4 | Click into the Description field and type a short string | Character count indicator may or may not appear (below threshold) |
| 5 | Continue typing in Description until approaching its character limit | Character count indicator appears, consistent with behavior on Description field |
| 6 | Click into the Welcome Message field and type a short string | Character count indicator may or may not appear (below threshold) |
| 7 | Continue typing in Welcome Message until approaching its character limit | Character count indicator appears, consistent with behavior on Welcome Message field |
| 8 | Compare count indicator behavior between Name, Description, and Welcome Message fields | All three fields show character count indicators at their respective thresholds, with consistent styling |

## Expected Final State

All three fields show character count indicators at their respective thresholds, with consistent styling

## Pass/Fail Criteria

**Pass:**
- Name field shows character count when at or near 32 characters
- Description and Welcome Message fields both show character count when approaching their limits
- Character count styling is visually consistent across all three fields

**Fail:**
- Name field never shows a character count indicator even when the limit is reached
- Inconsistency in character count display between Name and Description/Welcome Message fields
