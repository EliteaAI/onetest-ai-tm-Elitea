---
id: ELITEA-2429
title: "Skills editor back button returns to Skills list"
priority: medium
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: [tests.ui.skills.test_skill_back_navigation.test_back_button_from_skill_editor_returns_to_skills_list]
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1449
---

# ELITEA-2429: Skills editor back button returns to Skills list

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that Skills editor back button returns to Skills list. Success is confirmed when verify navigation goes to the skills list page and not to the chats page.

---

## Preconditions

- User is logged in to the Elitea platform.


---

## Test Data

| Field | Value |
|-------|-------|
| (none required) | — |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open any Skill for editing | Target page/section loads successfully. |
| 2 | Click the Back button in the Skill editor header | Control responds; expected next state is shown. |
| 3 | Verify navigation goes to the Skills list page and NOT to the Chats page | Condition holds as described. |

---

## Expected Final State

Verify navigation goes to the Skills list page and NOT to the Chats page.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Skills editor back button returns to Skills list.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
