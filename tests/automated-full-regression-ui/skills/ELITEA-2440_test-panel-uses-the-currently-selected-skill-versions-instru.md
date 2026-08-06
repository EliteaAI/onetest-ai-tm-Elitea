---
id: ELITEA-2440
title: "Test panel uses the currently selected Skill version's instructions"
priority: medium
type: functional
module: skills
status: ready
execution_type: automated
tags: [automated:UI:regression, feat:skills]
requirements: []
automation_test_id:
  - tests.ui.skills.test_skill_test_panel_version_instructions.TestSkillTestPanelVersionInstructions.test_test_panel_uses_selected_skill_version_instructions
automation_pr: https://github.com/EliteaAI/elitea-testing-public/pull/1266
---

# ELITEA-2440: Test panel uses the currently selected Skill version's instructions

**Module:** skills · **Priority:** medium · **Type:** functional

**Objective:** Verify that Test panel uses the currently selected Skill version's instructions. Success is confirmed when switch to "base" and run the same prompt — verify the response contains "base".

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
| 1 | Create a Skill with "base" instructions: "Always say BASE" | Operation completes successfully; state updates and confirmation is shown. |
| 2 | Save As Version "v1" with instructions: "Always say V1" | Operation completes successfully; state updates and confirmation is shown. |
| 3 | Switch to "v1" in the version selector | Action completes without error and produces the expected UI state. |
| 4 | Run test prompt: "What should you say?" | Action completes without error and produces the expected UI state. |
| 5 | Verify the response contains "V1" (not "BASE") | Condition holds as described. |
| 6 | Switch to "base" and run the same prompt — verify the response contains "BASE" | Action completes without error and produces the expected UI state. |

---

## Expected Final State

Switch to "base" and run the same prompt — verify the response contains "BASE".

---

## Pass/Fail Criteria

**Pass:**
- All steps complete without errors.
- The condition described in the title holds: Test panel uses the currently selected Skill version's instructions.

**Fail:**
- Any step produces an error or unexpected result.
- Any of the expected UI states, validations, or side effects is not observed.
