---
id: ELITEA-4336
title: "Verify Version filter returns accurate results in Run History"
priority: critical
type: functional
module: skills
status: ready
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6927]
---

## Preconditions

- User is logged in to `{{base_url}}`
- Skill has multiple versions (e.g., "base", "v1", "v2")
- Runs exist for each version

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills/all/[skillId]/history` |
| Versions | base, v1, v2 |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Navigate to Skill Run History page | Run History table displays all runs |
| 2 | Locate the version filter control | Version filter dropdown is visible |
| 3 | Note the available versions in the dropdown | All skill versions are listed (e.g., "base", "v1", "v2") |
| 4 | Select "base" version filter | Table updates to show only runs from "base" version |
| 5 | Verify all displayed runs show "base" in Version column | Version column shows "base" for all displayed runs |
| 6 | Change filter to "v1" version | Table updates to show only runs from "v1" version |
| 7 | Verify all displayed runs show "v1" in Version column | Version column shows "v1" for all displayed runs |
| 8 | Clear the version filter | Table returns to showing all runs regardless of version |

## Expected Final State

Version filter accurately filters run history by skill version, showing only runs from the selected version.

## Pass/Fail Criteria

**Pass:**
- Version filter control is accessible
- All skill versions are available in the dropdown
- Filtering by each version works correctly
- All displayed runs match the selected version
- Clearing the filter restores all runs

**Fail:**
- Version filter is missing or non-functional
- Not all versions are listed in the dropdown
- Runs with incorrect version are displayed
- Filtering does not update the table
