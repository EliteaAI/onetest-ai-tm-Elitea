---
id: ELITEA-3324
title: "Version selector allows choosing any combination of Agent versions for comparison"
priority: high
type: functional
module: agents
status: draft
execution_type: manual
tags: [feat:agents, r-2.0.6]
requirements: [EliteaAI/elitea_issues#6304]
---

## Preconditions

- User is logged in to `{{base_url}}` with edit permissions
- Agent exists with 4+ versions: base, v1.0, v2.0, v3.0

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/agents` |
| Version List | base, v1.0, v2.0, v3.0 (each with different Instructions text) |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open Compare Versions modal for Test Agent (4 versions) | Modal opens with default version selection (e.g., base vs latest) |
| 2 | Verify version dropdown/selector is available in Version 1 column header | Dropdown visible and clickable |
| 3 | Verify version dropdown/selector is available in Version 2 column header | Dropdown visible and clickable |
| 4 | Click Version 1 dropdown and select "base" | Dropdown expands, "base" is selectable |
| 5 | Click Version 2 dropdown and select "v3.0" | Version 2 column updates to show v3.0 content |
| 6 | Verify comparison now displays base vs v3.0 | Instructions and other fields show content from base and v3.0 |
| 7 | Change Version 1 to "v1.0" and Version 2 to "v2.0" | Comparison updates to v1.0 vs v2.0 |
| 8 | Verify content in both columns reflects the new version selection | Instructions text matches v1.0 and v2.0 |
| 9 | Select "v2.0" in BOTH Version 1 and Version 2 dropdowns | Both columns update to v2.0 |
| 10 | Verify comparison shows no differences (same version in both columns) | No diff highlighting visible, Instructions text identical |
| 11 | Navigate to User Interaction section | Section loads |
| 12 | Verify version selection persists (still v2.0 vs v2.0) | Version dropdowns show v2.0 in both columns |
| 13 | Change version selection to base vs v1.0 | Versions update |
| 14 | Navigate back to Instructions section | Section loads |
| 15 | Verify version selection persists across section navigation | Still shows base vs v1.0 |

## Expected Final State

Version selector allows selecting any two versions from the available list, comparison updates correctly, and version selection persists across section navigation.

## Pass/Fail Criteria

**Pass:**
- Version dropdowns available for both columns
- Can select any version from the list in each column
- Comparison content updates correctly after version change
- Can select same version in both columns (no diff)
- Version selection persists when navigating between sections

**Fail:**
- Version dropdowns missing or non-functional
- Cannot select certain versions
- Comparison content does not update after version change
- Error when selecting same version in both columns
- Version selection resets when navigating sections
