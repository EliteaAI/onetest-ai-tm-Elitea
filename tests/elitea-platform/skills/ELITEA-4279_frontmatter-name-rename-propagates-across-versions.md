---
id: ELITEA-4279
title: "Verify renaming a Skill via frontmatter name propagates across all versions"
priority: critical
type: functional
module: skills
status: draft
execution_type: manual
tags: [feat:skills, r-2.0.8]
requirements: [EliteaAI/elitea_issues#7125]
---

## Preconditions

- User is logged in to `{{base_url}}` with Editor or Admin role
- A Skill with 2+ versions exists

## Test Data

| Field | Value |
|-------|-------|
| URL | `{{base_url}}/app/skills` |
| New Name | `renamed-via-frontmatter` |

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Skill and switch to a non-base version | Non-base version loads with its own Instructions and the shared Name/Description |
| 2 | Edit the `name:` value in the frontmatter to a new valid value and Save (or Save As Version, per the version's edit rules) | Save completes successfully |
| 3 | Switch to a different version of the same Skill | Other version loads |
| 4 | Inspect the Name field and frontmatter `name` on that other version | Both reflect the new name |
| 5 | Check the Skill's entry in the Skills list | Skills list entry reflects the new name as well |

## Expected Final State

Renaming a Skill via its frontmatter on any version updates the Name for the Skill as a whole, visible consistently across all versions and in the Skills list.

## Pass/Fail Criteria

**Pass:**
- New name is reflected on every version of the Skill, and in the Skills list

**Fail:**
- New name only applies to the version where it was edited
- Other versions or the Skills list still show the old name
