---
id: ELITEA-1792
title: "Remove attached Skill from Agent"
priority: medium
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id: tests.ui.skills.test_remove_attached_skill_from_agent.TestRemoveAttachedSkillFromAgent.test_remove_attached_skill_from_agent
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/50
---

# ELITEA-1792: Remove attached Skill from Agent

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that an attached Skill can be removed from an Agent, that the removal is reflected in the Agent configuration after saving, and that the Skill itself remains intact in the Skills section.

---

## Preconditions

- User is logged in to the Elitea platform.
- A project exists and is accessible.
- The Skills and Agents sections are available in the project.
- An Agent exists with at least 2 Skills attached.

---

## Test Data

| Field | Value |
|-------|-------|
| Agent name | (any Agent with 2 Skills attached) |
| Skill to remove | "Skill B" (second attached Skill) |
| Skill to keep | "Skill A" (first attached Skill) |

---

## Steps

| # | Action | Expected Result |
|---|--------|-----------------|
| 1 | Open the Agent in edit mode that has "Skill A" and "Skill B" attached | Agent edit form is open; both Skills are listed as attached |
| 2 | Locate the remove/delete control for "Skill B" in the attached Skills list | Remove button or icon is visible for "Skill B" |
| 3 | Click the remove control for "Skill B" | "Skill B" is removed from the attached Skills list in the UI; "Skill A" remains |
| 4 | Save the Agent | Agent saves without errors |
| 5 | Reopen the Agent in edit or view mode | Agent shows only "Skill A" attached; "Skill B" is no longer listed |
| 6 | Navigate to the Skills section and verify "Skill B" still exists | "Skill B" is present in the Skills list and has not been deleted |

---

## Expected Final State

The Agent is saved with only "Skill A" attached. "Skill B" is no longer associated with the Agent but continues to exist as a standalone Skill in the project.

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- After saving, only "Skill A" is shown as attached to the Agent.
- "Skill B" still exists in the Skills section.

**Fail:**
- Any step produces an error or unexpected result.
- "Skill B" remains attached to the Agent after saving.
- "Skill B" is deleted from the Skills section as a side effect of removal.
