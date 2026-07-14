---
id: ELITEA-1739
title: "Search Skills by Name"
priority: medium
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: tests.ui.skills.test_skill_search.TestSkillSearch.test_search_skills_by_name
automation_pr: EliteaAI/elitea-testing-public#208
---

# ELITEA-1739: Search Skills by Name

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that the Skills list search by name supports partial matches, exact matches, non-existent name queries (empty state), and clearing the search to restore the full list.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills section is available in the project.

---

## Test Data

| Field | Value |
|-------|-------|
| Skill 1 name | Formatter |
| Skill 2 name | Code Reviewer |
| Skill 3 name | Content Writer |
| Partial search term | Co |
| Expected partial results | Code Reviewer, Content Writer |
| Exact search term | Formatter |
| Non-existent search term | (any name not matching the 3 skills, e.g. "Translator") |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Create 3 Skills with names: "Formatter", "Code Reviewer", "Content Writer" | All 3 Skills are created and visible in the Skills list |
| 2 | Search the Skills list by partial name "Co" | Only "Code Reviewer" and "Content Writer" are returned; "Formatter" is not shown |
| 3 | Search by the exact full name "Formatter" | Only the "Formatter" Skill is returned |
| 4 | Search by a non-existent name (e.g. "Translator") | An empty state is shown with no Skills listed |
| 5 | Clear the search field | All 3 Skills ("Formatter", "Code Reviewer", "Content Writer") are listed again |

---

## Expected Final State

The Skills list search correctly filters by name with partial and exact match support, shows empty state for non-matching queries, and restores the full list when the search is cleared.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- Partial search returns correct subset; exact search returns the correct single Skill; non-existent search shows empty state; clearing search restores all Skills.

**Fail:**
- Any step produces an error or unexpected result.
- Search returns incorrect results, does not filter the list, fails to show empty state, or does not restore the full list after clearing.

