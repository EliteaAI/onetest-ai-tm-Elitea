---
id: ELITEA-4239
title: Run button NOT visible in Skills list 3-dot menu
priority: critical
type: functional
module: elitea-platform
status: ready
execution_type: manual
tags: [feat:skills, skill-run, negative-test, skills-list, r-2.0.8]
requirements: [EliteaAI/elitea_issues#6922]
---
# ELITEA-4239: Run button NOT visible in Skills list 3-dot menu

**Module:** Elitea Platform · **Priority:** Critical · **Type:** Functional

**Objective:** Verify that "Run" action is NOT present in the 3-dot menu of user's own skills list (negative test - feature not implemented for own skills).

**Coverage:**
- Run action NOT in Skills list 3-dot menu
- Only Catalog skills have Run entry point
- Own skills do not have Run button

## Preconditions

- User is logged in to {{base_url}}
- User has at least one saved skill in their Skills list
- Skills list view is accessible

## Test Data

- User's own skill: Any skill in user's Skills list
- Expected: NO "Run" action in 3-dot menu

## Steps

| # | Action | Expected Result |
|---|--------|----------------|
| 1 | Navigate to Skills page | Skills page opens with list view |
| 2 | Locate any skill row in the list | Skill row displays with name, description, author, created date |
| 3 | Click the 3-dot menu (Actions) on the skill row | Dropdown menu opens with available actions |
| 4 | Observe the menu items | Menu shows: "Run", "Move to folder", "Delete" |
| 5 | Verify "Run" action is present in the menu | "Run" action IS visible in the menu for own skills |
| 6 | Click multiple different skill rows and check their 3-dot menus | All own skills show "Run" action in 3-dot menu |

## Expected Final State

"Run" action is present in 3-dot menu for user's own skills in list view.

## Pass/Fail Criteria

**Pass:** "Run" action appears in 3-dot menu for own skills; only existing actions like "Move to folder" and "Delete" are shown.

**Fail:** "Run" action is present in 3-dot menu when it should not be implemented for own skills.
