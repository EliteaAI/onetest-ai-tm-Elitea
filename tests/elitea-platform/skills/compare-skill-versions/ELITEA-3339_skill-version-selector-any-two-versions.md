---
id: ELITEA-3339
title: "Version selector allows choosing any combination of Skill versions for comparison"
priority: high
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Skill exists with 4+ versions: base, v1.0, v2.0, v3.0

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| Version List | base, v1.0, v2.0, v3.0 (each with different Instructions text) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Skill (4 versions) | Modal opens with default version selection (e.g., base vs latest) |
| 2 | Verify version dropdown/selector is available in Version 1 column header | Dropdown visible and clickable |
| 3 | Verify version dropdown/selector is available in Version 2 column header | Dropdown visible and clickable |
| 4 | Click Version 1 dropdown and select "base" | Dropdown expands, "base" is selectable |
| 5 | Click Version 2 dropdown and select "v3.0" | Version 2 column updates to show v3.0 content |
| 6 | Verify comparison now displays base vs v3.0 | Instructions show content from base and v3.0 |
| 7 | Change Version 1 to "v1.0" and Version 2 to "v2.0" | Comparison updates to v1.0 vs v2.0 |
| 8 | Verify content in both columns reflects the new version selection | Instructions text matches v1.0 and v2.0 |
| 9 | Select "v2.0" in BOTH Version 1 and Version 2 dropdowns | Both columns update to v2.0 |
| 10 | Verify comparison shows no differences (same version in both columns) | No diff highlighting visible, Instructions text identical |
| 11 | Change version selection back to base vs v1.0 | Versions update to show different content |
| 12 | Verify diff highlighting reappears for different versions | Differences are highlighted again |

## Expected Final State

Version selector allows selecting any two Skill versions from the available list, comparison updates correctly, and can compare same version in both columns.

## Pass/Fail Criteria

**Pass:**
- Version dropdowns available for both columns
- Can select any version from the list in each column
- Comparison content updates correctly after version change
- Can select same version in both columns (no diff)
- Diff highlighting updates based on version selection

**Fail:**
- Version dropdowns missing or non-functional
- Cannot select certain versions
- Comparison content does not update after version change
- Error when selecting same version in both columns
