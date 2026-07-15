---
id: ELITEA-1740
title: "Search Skills by Tag"
priority: medium
type: functional
module: search-and-tag-filtering
status: ready
execution_type: automated
automation_test_id: tests.ui.skills.test_skill_tag_filter.TestSkillTagFilter.test_filter_skills_by_tag
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/276
tags: [automated:UI:regression, feat:search]
requirements: []
---

# ELITEA-1740: Search Skills by Tag

**Module:** search-and-tag-filtering · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Skills list can be filtered by tag, returning only the skills that have the specified tag, and correctly handling tags shared across multiple skills as well as tags unique to a single skill.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills section is available in the project with tag-based filtering support.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill A name | (any name, e.g. "Skill A") |
| Skill A tags | `["formatting", "output"]` |
| Skill B name | (any name, e.g. "Skill B") |
| Skill B tags | `["formatting", "english"]` |
| Skill C name | (any name, e.g. "Skill C") |
| Skill C tags | `["translation"]` |
| Filter tag 1 | formatting |
| Filter tag 2 | translation |
| Filter tag 3 | output |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create Skill A with tags `["formatting", "output"]`, Skill B with tags `["formatting", "english"]`, and Skill C with tags `["translation"]` | All 3 Skills are created and visible in the Skills list with their respective tags |
| 2 | Filter/search Skills by tag `formatting` | Only Skill A and Skill B are returned; Skill C is not shown |
| 3 | Filter/search Skills by tag `translation` | Only Skill C is returned; Skills A and B are not shown |
| 4 | Filter/search Skills by tag `output` | Only Skill A is returned; Skills B and C are not shown |

---

## Expected Final State

The tag filter correctly narrows the Skills list to only those skills that have the specified tag, handling shared tags (returning multiple skills) and unique tags (returning a single skill) correctly.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Filtering by `formatting` returns Skills A and B only; by `translation` returns Skill C only; by `output` returns Skill A only.

**Fail:**
- Any step produces an error or unexpected result.
- Tag filter returns incorrect skills, includes skills without the specified tag, or excludes skills that have the specified tag.
